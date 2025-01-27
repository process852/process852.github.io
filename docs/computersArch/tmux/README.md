# [tmux](https://www.cs.swarthmore.edu/newhelp/tmux.html) 工具的基本使用

```bash
# 进入tumx模式
1. tumx
# 将一个终端划分水平两个子窗口
2. ctrl-b %
# 在左右两个子窗口切换
3. Ctrl-b 左/右方向键
# 退出子窗口或者整个tmux
4. Ctrl-d
```

每次命令`tmux`会触发一个新的会话(session)，会话会一直保持运行知道用户显式的关闭该会话。

## Detaching

如果想离开当前会话，但是保持会话持续运行，可以使用如下命令：
```bash
Ctrl-b d
```


## Attaching

既然存在多个后台运行的会话，就需要利用attach方式将后台会话附加至前台显式。

```bash
# 查看目前正在运行的会话
1. tumx ls
# 附加一个现有的会话，通过会话名或者会话编号
2. tumx attach -t <num>
2. tumx attach -t session-name
```

## Ending A session

```bash
# 前台运行的会话可以执行 Ctrl-d 退出所有
# 中止后台运行的会话方式
1. tmux kill-session -t <num>
1. tmux kill-session -t session-name
```

## tmux organization

`tmux`会创建一个session,每个session可以划分为多个windows，每个window内可以存在多个panes.

```bash
# 在当前pane下方新建新的pane
1. Ctrl-b "
# 在当前pane 右侧新建新的pane
2. Ctrl-b %
# 杀死当前pane
3. Ctrl-b x
```

## Window 操作

```bash
# 在当前会话(session)中创建新的窗口
1. Ctrl-b c
# 移动至前一个窗口
2. Ctrl-b p
# 移动至下一个窗口
3. Ctrl-b n
# 重命名一个窗口
4. Ctrl-b ,
```