# Mysql 示例

## 演示目标
* 创建一个 mysql 更新数据库的工单
* 完成一个工单的完整流程并查看状态

## 环境准备
```text
jira-servicedesk: 192.168.5.144:80

工单管理后台： 192.168.5.144:8080

jenkins: 192.168.5.151:8081

minio: 192.168.5.151:9000
AKIAIOSFODNN7EXAMPLE
wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY

adminer: 192.168.5.144:8089

mysql: 192.168.5.13:3306

awx: 192.168.5.151:80

jumpserver: https://local-jumpserver.arnoo.com/luna/

adminer: 192.168.5.144:8089

mysql: 192.168.5.13:3306

awx: 192.168.5.151:80

jumpserver: https://local-jumpserver.arnoo.com/luna/
```




要演示的数据库： iot_db_control_demo

演示的sql文件内容：
```mysql
INSERT IGNORE INTO iot_db_control_demo.device_attr_config(attr_name) VALUES('OnOff1'),('Dimming1'),('CCT1'),('RGBW1');
INSERT IGNORE INTO iot_db_control_demo.device_white_config(device_type_id) VALUES(-10031);
```
## 演示步骤：
查看演示前数据：
```mysql
use iot_db_control_demo;
select * from device_attr_config;
```
1. 用户林冲发起一个工单申请，这个工单的审批人是范超，提交后等待审批

2. 审批人范超审批通过此工单，等待运维林晨处理工单

3. 林晨接到审批通过的工单，点击 In Progress 开始处理工单

4. 林晨点击 In Progress 后会触发 Jenkins 作业
    - Jenkins 从 jira 工单中获取到相应信息，下载 jira 中的附件，并上传至minio中。
    - Ansible 从 minio 中下载相应的 sql 文件，先执行备份数据库操作，然后执行导入sql文件操作。
5. ansible 执行成功，jenkins修改 issue 状态为 SUCCESS,表示此工单成功完成
6. 由林晨关闭此工单，整个流程结束