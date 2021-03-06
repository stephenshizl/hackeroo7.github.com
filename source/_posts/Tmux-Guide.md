---
title: Tmux 简明指南
date: 2017-11-03 12:26:51
categories:
    - Tools
tags:
    - tmux
---

Tmux 做为一利器，很早就知道了，但是一直没有搞明白其使用场景，甚至一直在以错误的方式使用。现今花点时间搞明白它。

首先就是使用场景的问题，至于具体的命令以后在慢慢记忆。

<!--more-->

## 使用场景
1. 在远程机器上安装和使用 tmux。一般使用 SSH 登陆到远程机器上后，若 SSH 断开后，在重新登陆，但是原先的窗口中的输出啊什么的就看不到了。若 SSH 登陆后，使用 tmux 命令开启一个会话，就算 SSH 断开了，你在重新登陆后，直接 attach 到原先的会话，就回到了原先的工作现场。而且在会话的窗口中可以使用 tmux 的快捷键开启多个面板，不需要在来一个 SSH 连接过去了。在 SSH 登陆的时候，使用 `ssh user@host "command"` 或 `ssh user@host -- command`，直接在远程机器上执行命令，如 tmux。 
2. 在本地机器上安装使用 tmux。在本地使用的话，可以方便的分屏，在会话和终端中切换，减少窗口数量等。这些iTerm2 就可以啦，一般还是在远程机器上使用。不过 detach 后，倒是可以变相的隐藏窗口...

## Tmux 的使用
Ctrl + b，然后 d，就会从当前会话中分离，回到原先终端。在原先终端中 `tmux attach`，就可以来到原先的会话。

在 tmux 的会话中，按下 Ctrl + b 后是激活控制台，输入 ? 可以显示控制台命令帮助。

如果有多个会话，可以使用 `tmux ls` 查看，然后 `tmux attach -t sessionname` 进入到这个会话。

命令可以查看这个 [CheatSheet](https://gist.github.com/MohamedAlaa/2961058)

## Mac 上和 iTerm2 的集成
如果本地机器使用的是 iTerm2，在 SSH 远程连接中使用 `tmux -CC` 命令，一个新的 tmux 会话就会被创建，并会开启一个新的窗口，而且 iTerm2 会接管 tmux 的功能，如分屏，就无需使用 tmux 的命令来进行了，可直接在这个新的窗口中使用 iTerm2 的快捷键，还有如历史查找等快捷键，也没必要对远程机器进行单独配置这些了。关闭某个面板时，选择 Hide，就可以使用 `tmux -CC attach` 命令来 attach 了。这个依然是使用场景1。

在 iTerm2 的 `Preferences > general` 中有一项 `tmux Integration`，可以对集成的 tmux 进行一些设置，如打开新窗口做为本地 tab，执行 `tmux -CC attach` 后，隐藏本窗口等。

使用 mosh 替代 ssh，mosh 会自动断开重连，需要在两端都安装。不过若使用 mosh 的连接，使用 `-CC` 参数无反应。
