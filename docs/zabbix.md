# Zabbix 示例

## 演示目标
* 创建一个 zabbix agent 更新版本的工单
* 完成一个工单的完整流程并查看状态

## 环境准备
zabbix agent 升级版本 4.0.24-1


## 演示步骤：
演示前确认版本号
```shell script
ssh root@192.168.5.144
ssh root@192.168.5.36 
zabbix_agentd --version
```

1. 用户林冲发起一个工单申请，这个工单的审批人是范超，提交后等待审批

2. 审批人范超审批通过此工单，等待运维林晨处理工单

3. 林晨接到审批通过的工单，点击 In Progress 开始处理工单

4. 林晨点击 In Progress 后会触发 Jenkins 作业
    - Jenkins 从 jira 工单中获取要升级的版本号
    - Ansible 从私有yum仓库执行 yum update 操作。
5. ansible 执行成功，jenkins修改 issue 状态为 SUCCESS,表示此工单成功完成
6. 由林晨关闭此工单，整个流程结束