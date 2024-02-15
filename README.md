## Getting Started

> 声明：此项目只发布于 Github，基于 MIT 协议，免费且作为开源学习使用。并且不会有任何形式的卖号等行为，谨防受骗。

**LangChain4j-AiDeepin**
基于 ChatGPT 等大语言模型与 Langchain4j 等应用框架实现，开源、可离线部署的检索增强生成(RAG)大模型知识库项目。
功能：

* AI聊天
* AI生图
* 大模型知识库（RAG）

![1691585301627](image/README/1691585301627.png)

**AI聊天：**
![1691583184761](image/README/1691583184761.png)

![1691583124744](image/README/1691583124744.png)

![1691583329105](image/README/1691583329105.png)

**知识库：**
![kbindex](image/README/kbidx.png)

![kb01](image/README/kb01.png)

![kb02](image/README/kb02.png)

![kb03](image/README/kb03.png)

体验网址：[http://www.aideepin.com](http://www.aideepin.com/)

接入的模型：ChatGPT 3.5，DALL-E 2

该仓库为后端服务，前端项目见[langchain4j-aideepin-web](https://github.com/moyangzhan/langchain4j-aideepin-web)

### 技术

后端：

jdk17

springboot3.0.5

[langchain4j](https://github.com/langchain4j/langchain4j)

**Postgresql(需要安装[pgvector](https://github.com/pgvector/pgvector)扩展)**

前端：

vue3+typescript+pnpm

### 如何部署

#### 初始化

初始化数据库

* 创建数据库aideepin
* 执行docs/create.sql
* 填充openai的secret\_key

```plaintext
update adi_sys_config set value = 'my_chatgpt_secret_key' where name = 'secret_key'
```

* 修改配置文件

  * postgresql: application-[dev|prod].xml中的spring.datasource
  * redis: application-[dev|prod].xml中的spring.data.redis
  * mail: application.xml中的spring.mail

#### 编译及运行

* 进入项目

```plaintext
cd langchain4j-aideepin
```

* 打包：

```
mvn clean package -Dmaven.test.skip=true
```

* 运行

a. jar包启动：

```plaintext
cd adi-chat/target
nohup java -jar -Xms768m -Xmx1024m -XX:+HeapDumpOnOutOfMemoryError adi-chat-0.0.1-SNAPSHOT.jar --spring.profiles.active=[dev|prod] dev/null 2>&1 &
```

b. docker启动

```plaintext
cd adi-chat
docker build . -t aideepin:0.0.1
docker run -d \
  --name=aideepin \
  -e APP_PROFILE=[dev|prod] \
  -v="/data/aideepin/logs:/data/logs" \
  aideepin:0.0.1
```


### 待办：

接入基于ChatGLM的各种模型
