# Database design for EarnSpareMoney
## 概述
挣闲钱数据库主要由以下表组成
* users：用户信息表，存储用户信息
* missions： 任务表，储存任务信息
* operations： 用户参加表，表示用户参加某个活动
* questionnaires： 问卷列表，储存每个问卷的基本信息
* question_list: 问题列表，储存问卷中每个问题的内容
* choose_table: 选项列表，存储每个选项的内容
* choose_ops: 用户选择列表，储存用户选择的选项

## EER图
* 工具：mysql workbench

![](db_eer.jpg)
