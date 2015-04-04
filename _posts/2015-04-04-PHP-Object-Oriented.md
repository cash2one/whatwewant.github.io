---
layout: post
title: PHP 面向对象
category: php
tags: [php, Object-Oriented, OO, 面向对象]
---
{% include JB/setup %}

## 1. 面向对象(Object Oriented)基本概念
* 1. 对象的定义:
    * 世间万物皆对象: 可见和不可见之物
* 2. 对象的基本组成, 包含两部分:
    * 1. (属性，成员变量)对象的组成元素:
        * 是对象的`数据模型`，用于描述对象的数据
        * 又被称为对象的`属性`，或者对象的`成员变量`
    * 2. (方法)对象的行为:
        * 对象的`行为模型`, 用于描述对象能够做什么
        * 又被称为对象的`方法`
* 3. 对象的特点:
    * 1. 每个对象都独一无二
    * 2. 对象是体格特定事物,他的职能是完成特定功能
    * 3. 对象可以重复使用
* 4. 什么是面向对象:
    * 1. 向对象就是在编程的时候一直把对象放在心上
    * 2. 面向对象编程就是在编程的时候数据结构(数据组织方式)都通过对象的结构进行存储。:
        * 利用属性+方法存储数据
* 5. 为什么使用面向对象:
    * 1. 认识:
        * 1. (符合行为思维习惯)对象的描述方式更加贴近真实的世界，有利于大型业务的理解
        * 2. 在程序设计的过程中用对象的视角分析世界的时候能够拉近程序设计和真实世界的距离
    * 2. 实质:
        * 1. 面向对象就是把生活中要解决的问题都用对象的方式进行存储:
            * 属性 + 方法
        * 2. 对象与对象之间通过方法的调用完成互动:
            * 方法(的调用)
    * 3. 面向对象实例解析: 打篮球球员(对象) + 球员之间的互动(方法)
* 6. 面向对象的基本思路:
    * 1. 第一步: 识别对象:
        * 任何实体都可以被识别为一个对象
    * 2. 第二步: 识别对象的属性:
        * 对象里面存储的数据被识别为属性
        * 对于不同的业务逻辑，关注的数据不同，对象里面的属性也不同
    * 3. 第三步: 识别对象的行为(方法):
        * 对象自己属性数据的改变
        * 对象和外部交互
* 7. 面向对象的基本原则:
    * 1. 对象内部是高内聚的:
        * 对象只负责一项特定的职能(职能可大可小)
        * 所有对象相关的内容都封装到对象内部
    * 2. 对象对外是低耦合的: public, private, protected
        * 外部世界可以看到对象的一些属性(不是全部)
        * 外部世界可以看到对象的一些方法(并非全部)

## 2. PHP中的面向对象实践