# 概览

## 工单系统
工单系统是一个基于jira servicedesk, jenkins, ansible等工具构成的一套系统，为了记录，处理，跟踪一项服务升级的完成情况而设计的。

## 架构图
![avatar](img/cd.jpg)

## 特征
* 基于jira, 可记录，跟踪问题，扩展性强。
* jenkins 和 jira 集成，并且 jenkins 的插件丰富。
* 集成ansible，实现了批量系统配置、批量程序部署、批量运行命令等功能。