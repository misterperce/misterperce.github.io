---
layout: post
title: Simple scripting with AutoHotKey
---

I'm currently in a role in which I have to navigate and explore a lot of new SQL tables that I'm not familiar with, so I found myself typing "select * from ... limit 100" over and over again. I finally decided to automate that phrase such that if I typed "sss" it would automatically type "select * from  limit 100". I couldn't be happier with the results. This is how I did it:

I used the program AutoHotKey — my company had this in their software library so I installed it via that.

My script looks like this:
```
#NoEnv ; Recommended for performance and compatibility with future AutoHotkey releases.
#Warn ; Enable warnings to assist with detecting common errors.
SendMode Input ; Recommended for new scripts due to its superior speed and reliability.
SetWorkingDir %A_ScriptDir% ; Ensures a consistent starting directory.
::
   :*:sss::select * from  limit 100
Return
```
The one gotcha I ran into was having to run, or enable, the script every single time I logged in. Fortunately, I found a solution.

Original answer here: [https://superuser.com/questions/1281982/autohotkey-script-not-running-on-startup/1306304#1306304](https://superuser.com/questions/1281982/autohotkey-script-not-running-on-startup/1306304#1306304)

Edit the startup registry directly:

1. Run regedit
2. Browse to
Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
3. Add new String Value
4. For Value Data, input path to your .ahk file
