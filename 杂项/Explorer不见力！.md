---
profileName: Estruswent
postId: "1767"
postType: post
categories:
  - 1
---
## 问题描述
Explorer.exe不知名抽风导致我找不到我的子系统
在windows powershell中输入`start explorer`或`explorer`出现报错信息：
`shell:::{52205fd8-5dfb-447d-801a-d0b52f2e83e1}`找不到应用程序
## 解决方案：
### 方案一：
修改注册表，但存在风险，不过一劳永逸，参考以下链接。
https://www.tenforums.com/tutorials/127506-add-remove-linux-navigation-pane-windows-10-a.html
### 方案二：
在左下角运行处用命令行`\\wsl$`就进入我的Ubuntu了，不过子系统不显示的问题还是存在......而且不知道其他子系统下怎么处理这一情况