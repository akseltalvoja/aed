---
title: Docker Stop All Containers
feed: show
date: 2026-03-10
---

*Use this when the system is struggling under the weight of orphaned containers.*
```batch
@echo off
echo Too lazy to stop all the running containers? fine...
FOR /F %%i IN ('docker ps -q') DO docker stop %%i
echo Done.
pause
```
---

*"I’m not lazy, I’m just highly motivated to do nothing efficiently."
— Anonymous* 