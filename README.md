#安装虚拟机
```sh
docker run --name EXPRESS -p8188:8188\
  -v /bigdata/SITES/:/www/ \
  -it -d node:18.15.0-bullseye
```

#进入容器
```sh
docker exec -it EXPRESS bash
```

- 安装vi
```sh
  echo 'deb https://mirrors.tencent.com/debian/ bullseye main'                    > /etc/apt/sources.list   &&\
  echo 'deb https://mirrors.tencent.com/debian-security/ bullseye-security main' >> /etc/apt/sources.list   &&\
  echo 'deb https://mirrors.tencent.com/debian/ bullseye-updates main'           >> /etc/apt/sources.list   &&\
apt update && apt install -y vim
```

- 0到1初始化项目
```sh
mkdir /www/hello-express && cd /www/hello-express && \
  npm init -y && \
  npm i express
```

- git该项目
```sh
echo '/node_modules' >.gitignore && \
  git init && git add . && \
  git commit -m init && git branch -m master
```

- 0-1实现该项目
  ```sh
  vi app.js
  ```

```js
const express = require('express');
const app = express();
const port = 8188;

// 使用 express.static 中间件来处理静态文件
app.use(express.static('public'));

// 设置路由
app.get('/', (req, resp) => {
  resp.send('Hello World!');
});

// 启动服务器
app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});

```

- git该项目
```sh
mkdir public && \
  echo '*'            >public/.gitignore && \
  echo '!.gitignore' >>public/.gitignore && \
git add . && git commit -m impl
```

- 启动应用
```sh
npm i -g pm2 && pm2 start --name hello-express app.js
```
