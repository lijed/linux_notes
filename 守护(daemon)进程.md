# 守护进程

Linux中的daemon进程（也称为守护进程或后台进程）是在后台长时间运行的进程，它们通常在系统启动时自动启动，并在系统关闭时自动关闭。这些进程不占用控制终端，也不与用户进行直接交互，主要用于执行后台任务，如服务器服务、监控系统等。关于Linux daemon进程相关的日志，以下是一些关键信息：

- ### 1. 日志守护进程
  - **syslog**：大部分Linux发行版默认的日志守护进程为syslog（或其变种如rsyslog、syslog-ng等），这些守护进程负责接收来自系统和其他程序的日志信息，并将其保存到指定的日志文件中。

- ### 2. 日志文件位置
  - 日志文件通常保存在`/var/log`目录下。这个目录包含了多种类型的日志文件，用于记录系统、服务和应用程序的各种事件和错误。

- ### 3. 常用日志文件

  与daemon进程相关的日志文件可能包括但不限于以下几种：

  - **/var/log/messages**：记录Linux操作系统常见的系统和服务错误信息（在某些系统中，此功能可能由`/var/log/syslog`承担）。
  - **/var/log/secure**：Linux系统安全日志，记录用户和工作组变化情况、用户登录认证情况等与安全相关的日志信息。
  - **/var/log/syslog** 或 **/var/log/rsyslog**：根据配置，这些文件可能包含所有系统活动的日志信息，包括daemon进程的输出。
  - **/var/log/服务名.log**：对于特定的daemon进程，如Apache、Nginx等，它们可能会将日志信息写入以服务名命名的日志文件中，如`/var/log/apache2/access.log`、`/var/log/nginx/error.log`等。

- ### 4. 日志配置

  - 日志的配置通常通过syslog的配置文件来完成，这些文件可能名为`/etc/syslog.conf`、`/etc/rsyslog.conf`或`/etc/rsyslog.d/`目录下的文件。通过编辑这些配置文件，可以指定不同类别和优先级的日志信息保存到哪些文件中。

- ### 5. 查看日志

  - 可以使用`cat`、`tail`、`grep`等命令来查看和分析日志文件。例如，`tail -f /var/log/syslog`命令可以实时查看`/var/log/syslog`文件的末尾内容，这对于监控系统的实时状态非常有用。

  ### 6. 注意事项

  - 日志文件可能包含敏感信息，因此应该只有授权用户才能访问这些文件。
  - 随着时间的推移，日志文件可能会变得非常大，从而占用大量磁盘空间。因此，需要定期清理或轮转这些日志文件。

  总之，Linux daemon进程相关的日志是系统管理和安全监控的重要组成部分。通过合理配置和定期查看这些日志文件，管理员可以及时发现并解决问题，确保系统的稳定运行。

- 使用nohup 与 &符号配置运行一个命令
  - nohup命令使命令进程忽略hangup(挂起)信号
- 守护进程 和一般进程有什么区别呢
- 使用screen命令
  - screen进入screen环境
  - ctrl + a d 退出 detached screen环境
  - screen -ls 查看screen的会话
  - screen -r sessionID 恢复会话





## screen

### screen 安装

```shell
yum install  screen 
```



## 日志

/var/log/messages  daemon进行后台运行的日志

dmesg 内核日志

secure 

cron 定时任务的执行日志