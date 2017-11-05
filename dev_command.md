#about dev command#
***

##screen##

1. 创建screen会话

        screen -S lnmp(screen会创建一个名字为lnmp的会话)

2. 暂时离开screen会话

        ctrl+a d

3. 恢复screen会话

        screen -ls(查看会话列表)
        screen -r 会话id

4. 关闭会话

        exit

5. 远程演示

        screen -x 会话id

6. 常用快捷键

        ctrl+a c:在当前的会话中创建窗口
        ctrl+a w:窗口列表
        ctrl+a n:下一个窗口
        ctrl+a p:上一个窗口
        ctrl+a 0-9:在第一个窗口和第9个窗口之间切换

7. 分屏

        ctrl+a S:(大S,水平分屏)
        ctrl+a |:(垂直分屏)
        注:
        在新建的空的分屏中ctrl+a n会出现镜像屏

##tmux##