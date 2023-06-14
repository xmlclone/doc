- [基础命令](#基础命令)
- [配置](#配置)
  - [免密访问](#免密访问)

# 基础命令

```shell
# 创建用户(默认会在/home目录下创建testuser的home目录)
useradd testuser
# 设置密码(更改密码)
passwd testuser


# 查看系统信息
uname -a
uname -r # 查看系统位数
cat /proc/version
```

# 配置

## 免密访问

假设A要远程访问B

```shell
# A机器上
# 设置主机名(每个机器都需要配置，至少不能是localhost之类的)
vi /etc/hostname
# 设置后需要重启生效
reboot
# 下面命令会在指定目录下(执行命令会有提示)生成id_rsa.pub文件
# 找到生成的pub文件，并把内容复制下来
ssh-keygen -t rsa

# B机器上
# 同样执行上面的命令，如果对应的文件已经有了则不需要执行
# 进入到id_rsa.pub文件所在目录下，编辑或创建authorized_keys文件，把A机器id_rsa.pub文件内容复制到此文件内
# authorized_keys文件可以有多个，注意换行操作
```