---
layout: post
title: "Domain modeling"
description: 领域建模实践.
image: 'https://www.codebydesign.com/SystemArchitect/ScreenShots/XP/PhysicalModel.png'
category: 'blog'
tags:
- software-system-analysis-and-design
- domain
- modeling
twitter_text: 领域建模实践.
introduction: 领域建模实践.
---

# 领域建模实践

------

## 1. 领域建模
 - a. 阅读 Asg_RH 文档，按用例构建领域模型。
    - 按 Task2 要求，请使用工具 UMLet，截图格式务必是 png 并控制尺寸
    - 说明：请不要受 PCMEF 层次结构影响。你需要识别实体（E）和 中介实体（M，也称状态实体）
        - 在单页面应用（如 vue）中，E 一般与数据库构建有关， M 一般与 [store](https://cn.vuejs.org/v2/guide/state-management.html) 模式 有关
        - 在 java web 应用中，E 一般与数据库构建有关， M 一般与 session 有关
    
    ![Asg_RH Task2 领域模型](/assets/img/blog/domain-modeling-reserve-hotel.png)
 - b. 数据库建模(E-R 模型)
    - 按 Task 3 要求，给出系统的 E-R 模型（数据逻辑模型）
    - 建模工具 PowerDesigner（简称PD） 或开源工具 [OpenSystemArchitect](https://www.codebydesign.com)
    - 不负责的链接 [http://www.cnblogs.com/mcgrady/archive/2013/05/25/3098588.html](https://www.qunar.com)
    - 导出 Mysql 物理数据库的脚本
    - 简单叙说 数据库逻辑模型 与 领域模型 的异同
        - E-R 模型
        
        ![Asg_RH Task1 用例图](/assets/img/blog/domain-modeling-design.png)

        - Mysql 物理数据库的脚本
            ```sql
            -- +---------------------------------------------------------
            -- | MODEL       : Northwind
            -- | AUTHOR      : 
            -- | GENERATED BY: Open System Architect
            -- +---------------------------------------------------------
            -- | WARNING     : Review before execution
            -- +---------------------------------------------------------

            -- +---------------------------------------------------------
            -- | CREATE
            -- +---------------------------------------------------------
            CREATE TABLE `Loction`
            (
            code INTEGER NOT NULL,
            name VARCHAR(40) NOT NULL,
            PRIMARY KEY (code)
            );

            CREATE TABLE `Hotel`
            (
            name CHAR(1024) NOT NULL,
            star_rating INTEGER,
            PRIMARY KEY (name)
            );

            CREATE TABLE `Reservation`
            (
            hotel_name VARCHAR(1024) NOT NULL,
            room VARCHAR(30),
            price REAL(30),
            check_in_date DATE,
            check_out_date DATE
            );

            CREATE TABLE `Room`
            (
            NO. INTEGER,
            PRIMARY KEY (NO.)
            );

            CREATE TABLE `Traveler`
            (
            ID INTEGER NOT NULL,
            name VARCHAR(40),
            address VARCHAR(60),
            email VARCHAR(15),
            PRIMARY KEY (ID)
            );
            ```
        - 数据库逻辑模型 与 领域模型 的异同
            - 不同：领域模型用于分析，而数据库模型用于开发，需要给出更具体细节，如字段类型。
            - 相同：表达实体、中介之间的关系(约束)。