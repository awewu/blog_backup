---
title: Drools_1.简单介绍
cover: /my_pic/Drools/0.png
date: 2022-1-12 22:44:32
tags: ['Drools', 'Java']
categories: ['后端']
toc: true
---

# Drools_1.简单介绍

## 1、引入

在日常开发中，经常会用各种 **规则** 引导我们的程序，比如：某公司的日常促销规则如下：

```text
订单金额小于 10 万元（不包含），正常提货不打折
订单金额在 10 万到 50 万（不包含）之间，打 8 折
订单金额在 50 万到 100 万（不包含）之间，打 6 折
订单金额在 100 万以上，打 5 折
```

直接用 `Java` 编写就是下面这样

```java
/**
 *	获取订单折扣
 *	@param order 订单对象
 */
public void getDiscount(Order order) {
    
	if (order.getMoney() >= 100000 && order.getMoney() < 500000) {
        // 设置折扣
        order.setDiscount(8);
    } else if (order.getMoney() >= 500000 && order.getMoney() < 1000000) {
        // 设置折扣
        order.setDiscount(6);
    } else if (order.getMoney() >= 1000000) {
        // 设置折扣
        order,setDiscount(5);
    }
    
}
```

但是一旦公司搞活动，修改了相应的促销政策，那就势必需要在代码里面对业务规则进行修改和维护，然后重新编译生成服务。这样就会带来不必要的开销。

所以，为了应对以上的问题，产生了一种叫 **规则引擎** 的概念。其通过将 **业务代码** 与 **规则** 剥离开来，方便后期修改与维护。而 `Drools` 就是一种 **规则引擎**。（*官网：https://www.drools.org/*）

>  **规则引擎**，全称为 **业务规则管理系统**，英文名为 `BRMS`(即 `Business Rule Management System`)。规则引擎的主要思想是将应用程序中的业务决策部分分离出来，并使用预定义的语义模块编写业务决策（业务规则），由用户或开发者在需要时进行配置、管理。 

## 2、案例

`Drools` 的开发步骤如下：

![1](/my_pic/Drools/1.简单介绍/1.png)

### 2.1、创建项目

创建一个 `maven` 项目，并引入以下包

```xml
<dependency>
    <groupId>org.drools</groupId>
    <artifactId>drools-compiler</artifactId>
    <version>7.10.0.Final</version>
</dependency>
<!--junit是为了测试用-->
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
</dependency>
```

### 2.2、创建配置文件

配置文件需要创建在 `resources/META-INF/kmodule.xml` 中，其固定写法见下：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<kmodule xmlns="http://www.drools.org/xsd/kmodule">
    <!--
        name：指定kbase的名称，可以任意，但是需要唯一
        packages：指定规则文件的目录，需要根据实际情况填写，否则无法加载到规则文件
        default：指定当前kbase是否为默认
    -->
    <kbase name="kbase1" packages="rules" default="true">
        <!--
            name：指定ksession名称，可以任意，但是需要唯一
            default：指定当前session是否为默认
        -->
        <ksession name="session-rule" default="true"/>
    </kbase>
</kmodule>
```

**`kmodule`：**可以包含一个或多个 `kbase`，分别对应 `drl` 规则文件

**`packages`：**为 `drl` 文件在 `resources` 目录下的路径，多个包用逗号分隔，默认情况下会扫描 `resources` 目录下 **所有**（包含子目录）的规则文件

**`kbase`：**中的 `default` 属性表示该 `KieBase` 是否是默认的。如果是默认的，则不用名称就可以查找到该 `KieBase`，每个 `kmodule` 最多只能有一个默认的 `KieBase`。`kbase` 下可以有多个 `ksession`

### 2.3、创建对象

创建订单如下，因为只涉及订单金额和订单折扣，所以我们暂时就只写这两个字段

```java
public class Order {
    
    // 订单金额
    private int amount;
    // 订单折扣
    private double discount;

    @Override
    public String toString() {
        return "Order{" +
                "amount=" + amount +
                ", discount=" + discount +
                '}';
    }

    public int getAmount() {
        return amount;
    }

    public void setAmount(int amount) {
        this.amount = amount;
    }

    public double getDiscount() {
        return discount;
    }

    public void setDiscount(double discount) {
        this.discount = discount;
    }
}
```

### 2.4、创建 `drl` 配置文件

根据 `kmodule.xml` 中设置的 `kbase` 的 `packages`，在 `resources` 下创建相应目录，然后在该目录下创建 `drl` 文件

在 `drl` 文件中根据相应的规则进行配置

```drl
package  awewu.rules;

import io.github.awewu.Order;

rule "discount_lv1"
when
    $order:Order(amount < 100000)
then
    $order.setDiscount(10);
    System.out.println("规则触发：订单金额在100000以内，没有折扣");
end

rule "discount_lv2"
when
    $order:Order(amount >= 100000 && amount < 500000)
then
    $order.setDiscount(8);
    System.out.println("规则触发：订单金额在100000到500000之内，打8折");
end

rule "discount_lv3"
when
    $order:Order(amount >= 500000 && amount < 1000000)
then
    $order.setDiscount(6);
    System.out.println("规则触发：订单金额在500000到1000000之内，打6折");
end

rule "discount_lv4"
when
    $order:Order(amount >= 1000000)
then
    $order.setDiscount(5);
    System.out.println("规则触发：订单金额大于1000000，打5折");
end
```

### 2.5、编写单元测试

```java
@Test
public void testOrderDrools() {
    // 获取 KieServices
    KieServices kieServices = KieServices.Factory.get();
    // 获取 KieContainer
    KieContainer container = kieServices.getKieClasspathContainer();
    // 获取 KieSession
    KieSession kieSession = container.newKieSession();
    // 获取事实对象
    Order order = new Order();
    order.setAmount(199999);
    kieSession.insert(order);
    // 执行并触发规则
    kieSession.fireAllRules();
    // 关闭 KieSession
    kieSession.dispose();
    
    System.out.println("执行之后，订单折扣是：" + order.getDiscount());
}
```



