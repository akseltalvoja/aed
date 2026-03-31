---
title: Docker Delete All Containers
feed: show
date: 2026-03-10
---

*Total wipe of all containers. Use when RAM usage becomes a threat to stability.*
```batch
@echo off
echo Stopping ALL running Docker containers...
FOR /F %%i IN ('docker ps -q') DO docker stop %%i

echo.
echo Deleting ALL Docker containers...
FOR /F %%i IN ('docker ps -aq') DO docker rm %%i

echo.
echo Done. Your RAM is safe... for now.
pause
```
---

*"I’m not lazy, I’m just highly motivated to do nothing efficiently."
— Anonymous* 