# collect_service_ip_port_to_yed
====
收集服务信息导入数据库，然后根据连接socket情况分析导出为EXCEL，使用yed自动生成服务架构图。
使用saltstack推送。
----

----
        收集信息=》存储
        yum install -y python-netifaces MySQL-python

        2017-02-27
            2.6.6版本不支持subprocess.check_out,修改为subprocess.Popen(["ls", "-a"], stdout=subprocess.PIPE).communicate()[0]
        2017-02-28
            使用re重写shell命令部分
            重写数据导入方法
            优化端口扫描方式，节省2/3时间
        2017-03-01
            解决插入数据重复问题
            改写appcolect为类方法
            调整数据录入逻辑
            ip地址不同版本系统获取问题
        2017-03-10
            去掉127.0.0.1监听地址防止端口相同的业务出现错误
        2017-03-13
            程序匹配更多的项目类型，不仅限于java类的tomcat
        2017-03-14
            使用配置文件添加项目匹配。
        2017-03-15
            添加帮助，版本，配置文件等信息
        2017-03-16
            修复porjectname过长被truncate的问题
        2017-03-21
            添加记录原始数据日志功能
            收集完监听pid未处理连接池之间，进程重启有一定机率匹配到其它启动起来占用原来pid，造成匹配信息错误。
            添加pid创建日期判断
        2017-03-22
            listen port, pool ip port去重，节约处理时间
        2017-03-27
            使用multi-threads多线程处理
        未解决：
            使用psutil模块代替ps,ss收集信息。
            使用日志模块记录日志