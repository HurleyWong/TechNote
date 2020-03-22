## Mac OS设置Finder显示隐藏文件

1. 进入终端，输入命令：

    ```powershell
     // 设置隐藏文件不可见
     defaults write com.apple.finder AppleShowAllFiles FALSE
     // 设置隐藏文件可见
     defaults write com.apple.finder AppleShowAllFiles TRUE
    ```

2. 在终端输入命令重启Finder后才能修改

    ```powershell
     killall Finder
    ```

