## Ubuntu文件复制权限问题

打开终端，输入命令

```powershell
sudo chmod 777 /usr/share/themes
```

即 sudo chmod 777 加上要复制到的路径

- sudo chmod 600 xxx  （只有所有者有读和写的权限）
- sudo chmod 644 xxx  （所有者有读和写的权限，组用户只有读的权限）
- sudo chmod 700 xxx （只有所有者有读和写以及执行的权限）
- sudo chmod 666 xxx （每个人都有读和写的权限）
- sudo chmod 777 xxx （每个人都有读和写以及执行的权限）