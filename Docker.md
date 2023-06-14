- [基础命令](#基础命令)
- [Dockerfile](#dockerfile)

# 基础命令

```shell
# 保存镜像
docker save -o nginx.tar nginx:latest

# 导入镜像
docker load -i nginx.tar
```

# Dockerfile

文件名就叫Dockerfile

```dockerfile
FROM python:3.9-bullseye

COPY msyh.ttc /usr/share/fonts

COPY chromedriver_102.0.5005.61 /usr/bin/chromedriver
WORKDIR /opt
RUN apt update
COPY google-chrome-stable_current_amd64_102.0.5005.115.deb /opt/google-chrome-stable_current_amd64.deb 
RUN dpkg -i google-chrome-stable_current_amd64.deb || true
RUN apt-get -y -f install
RUN dpkg -i google-chrome-stable_current_amd64.deb

WORKDIR /usr/src/app
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple/
RUN sed 's/maxsize=1,/maxsize=100,/' -i /usr/local/lib/python3.9/site-packages/urllib3/connectionpool.py

ADD entrypoint.sh /opt

WORKDIR /opt/mrtctest

ENTRYPOINT ["sh" ,"/opt/entrypoint.sh"]
CMD ["scripts/dory_case_demo.py", "--no-statis"]
```

最后使用`docker build -t xxx:vx.x .`命令即可生成镜像