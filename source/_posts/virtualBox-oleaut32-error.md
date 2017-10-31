---
title: PSDispatch looks broken by some installer featuring the broken oleaut32.msm module as a component.
date: 2017-10-12 15:54:03
---

## 启动VirtualBox时报错
1. PSDispatch looks broken by some installer featuring the b
roken oleaut32.msm module as a component.
2. Failed to instantiate CLSID_VirtualBox w/ IVirtualBox, but CLSID_VirtualBox w/ IUnknown works.

## 解决办法：
` 1. win+r 快捷键打开 “运行”，输入regedit 打开注册表 `

` 2. 找到 HKEY_CLASSES_ROOT\CLSID\{00020420-0000-0000-C000-000000000046} InprocServer32 修改 第一行（默认）的值为 C:\Windows\system32\oleaut32.dll`

` 3. 找到HKEY_CLASSES_ROOT\CLSID\{00020424-0000-0000-C000-000000000046} InprocServer32  修改 第一行（默认）的值为 C:\Windows\system32\oleaut32.dll `

` 4. 重启VirtualBox `

