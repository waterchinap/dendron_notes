---
id: nmk7uy47cezvv1sa5ckzxz8
title: Python 开发全流程总结
desc: ''
updated: 1662565912902
created: 1662565912902
isDir: false
---
- #python
# 1. 开发环境
## linux
manjaro
## IDE
最好的IDE是pycharm
jupyer lab好用的EDA工具
## python环境管理
poetry
# 2. web开发框架
## fastapi
速度快
## flask
文档多
## 向golang演进？
# 3. 项目开发
## 面向对象
各个模块之间保持松耦合。
## 设计模式
# 4. 部署
## 准备
使用poetry导出requirements.txt
清理不必要的包。（应该在开发时，把不必要的包打上test标签）
```bash
poetry update  # 更新，导出前poetry要求update
poetry export -o requirement --without-hashes
```
## docker
### Dockerfile
```dockerfile
FROM python:3.8

LABEL maintainer="eric peng"

WORKDIR /usr/src/app

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

# 注意目录结构
COPY . .

EXPOSE 8000

CMD [ "uvicorn", "fastapi_covid.main:app", "--host", "0.0.0.0", "--port", "8000" ]
```
### build image
```bash
docker build -t my-python-app .
# 注意最后的点号，表示当前目录。
```
### 运行
```bash
docker run -it --rm -p 8000:8000 --name fastcontainer fastimg
# 注意几个参数的作用， -d 后台运行。
```
## docker-compose
后续结合github，docker-compose，应用于数据库和web结合的项目。