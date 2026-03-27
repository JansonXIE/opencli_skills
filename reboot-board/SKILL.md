---
name: reboot-board
description: "重启开发板。Use when: 用户需要重启板端、reboot board、板子重启、串口重启。清空启动日志并通过串口发送 reboot 命令。"
argument-hint: "直接调用即可，无需参数"
---

# 重启开发板

## 功能
通过串口 `/dev/ttyUSB0` 向开发板发送 reboot 命令，并在重启前清空启动日志 `board_boot.log`。

## 前置条件
- 终端中已设置环境变量 `SUDO_PASS`（sudo 密码）
- 串口设备 `/dev/ttyUSB0` 已连接

## 执行步骤

严格按以下顺序在终端中执行：

### 第 1 步：清空启动日志
```bash
echo "$SUDO_PASS" | sudo -S sh -c '> board_boot.log'
```

### 第 2 步：发送重启命令
```bash
echo "$SUDO_PASS" | sudo -S bash -c 'echo -e "reboot\r" > /dev/ttyUSB0'
```

## 注意事项
- 如果环境变量 `SUDO_PASS` 未设置，先提示用户在终端中执行 `export SUDO_PASS="你的密码"` 进行设置
- 两条命令必须按顺序执行，先清日志再发重启
- 若串口设备路径不同，用户可指定替代路径
