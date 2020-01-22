### Dockerfile常用命令

在之前编写Nginx镜像时，用到了FORM、RUN指令。事实上，Dockerfile有十多个指令。指令的一般格式为：指令名称 参数。

1. ADD复制文件，格式为：

   - `ADD <src>... <dest>`
   - `ADD ["<src>",... "<dest>"]`

   从src目录复制文件到容器的dest。其中src可以是Dockerfile所在目录的相对路径，也可是URL，也可是压缩包。

   注意：

   - src必须构建在上下文内，不能使用如：ADD ../somethine /something这样的命令，因为docker build首先会将上下文路径和其子目录发送到docker daemon
   - 如果src是一个URL，同时dest不以斜杠结尾，dest会被视为文件，src对应内容会被下载到dest。如果以斜杠结尾，dest会被视为目录，src对应内容会被下载到dest目录
   - 如果src是一个目录，那么整个目录下的内容会被复制，包括文件系统元数据
   - 如果文件是可识别的压缩包，docker会自动解压

   示例：

   ```
   ADD microservice-discovery-eureka-0.0.1-SNAPSHOT.jar app.jar
   ```

2. ARG设置构建参数，格式为：

   `ARG <name>[=<default value>]`

   示例：

   ```
   ARG user1=someuser
   ```

3. CMD容器启动命令，格式为(支持三种格式)：

   - `CMD ["executable","param1","param2"]`，(推荐使用)
   - `CMD ["param1","param2"]`，(为ENTRYPOINT指令提供预设参数)
   - `CMD command param1 param2`，(在shell中执行)

   CMD用于为执行容器提供默认值。每个Dockerfile只有一个CMD命令，如果指定多个，最终只有最后一个会被执行，如果启动容器时指定了运行的命令，则会覆盖CMD指定的命令。

   示例：

   ```
   CMD echo "This is a test." | wc -
   ```

4. COPY复制文件，格式为：

   - `COPY <src>... <dest>`
   - `COPY ["<src>",... "<dest>"]`

   复制本地的src到容器的dest。COPY和ADD类似，COPY不支持URL和压缩包。

   示例：

   ```
   COPY package.json /usr/src/app/
   ```

5. ENTRYPOINT入口点，格式为：

   - `ENTRYPOINT ["executable","param1","param2"]`
   - `ENTRYPOINT command param1 param2`

   ENTRYPOINT和CMD指令的目的一样，都是指定Docker容器启动时执行的命令。

6. ENV设置环境变量，格式为：

   - `ENV <key> <value>`
   - `ENV <key>=<value> ...`

   示例：

   ```
   ENV JAVA_HOME /path/to/java
   ```

7. EXPOSE声明暴露的端口，格式为：

   `EXPOSE <port> [<port>...]`

   需注意的是，这只是一个声明，运行时不会因为该声明打开相应端口。主要是帮助镜像使用者理解该镜像服务的守护端口；其次是运行时使用随机映射时，会自动映射EXPOSE的端口。

   示例：

   ```
   #声明暴露一个端口
   EXPOSE port1
   #相应的运行容器使用的命令
   docker run -p port1 image
   #也可使用-P选项启动
   docker run -P iamge
   
   #声明暴露多个端口
   EXPOSE port1 port2 port3
   #相应的运行容器使用的命令
   docker run -p port1 -p port2 -p port3 image
   #也可指定需要映射到宿主机上的端口号
   docker run -p host_port1:port1 -p host_port2:port2 -p host_port3:port3 image
   ```

8. FROM指定基础镜像，格式为(支持三种格式)：

   - `FROM <image>`
   - `FROM <image>:<tag>`
   - `FROM <image>@<digest>`

   FROM指令有点像Java里的 extends 关键字。需注意的是，FROM指令必须指定且需写在其他指令之前。FROM指令后的所有指令都依赖于该指令所指定的镜像。

9. LABEL为镜像添加元数据，格式为：

   `LABEL <key>=<value> <key>=<value> ...`

   使用 " 和 \ 转换命令行

   示例：

   ```
   LABEL "com.example.vendor"="ACME Incorporated"
   LABEL com.example.label-with-value="foo"
   LABEL version="1.0"
   LABEL description="This text illustrates \
   that label-values can span multiple lines."
   ```

10. MAINTAINER指定维护者的信息，用于为docker署名，格式为：

    `MAINTAINER <name>`

    示例：

    ```
    MAINTAINER zp<qwea1@136.com>
    ```

11. RUN执行命令，格式为：

    - `RUN <command>`
    - `RUN ["executable","param1","param2"]`

12. USER设置用户，格式为：

    `USER 用户名`

    该指令用于设置启动镜像时的用户或者UID，写在该指令后的RUN、CMD以及ENTRYPOINT指令都将使用该用户执行命令。

    示例：

    ```
    USER daemon
    ```

13. VOLUME指定挂载点，格式为：

    `VOLUME ["/data"]`

    该指令使容器中的一个目录具有持久化存储的功能，该目录可被容器本省使用，也可共享给其他容器。当容器中的应用持久化数据的需求时可以在Dockerfile中使用该指令。

    示例：

    ```
    VOLUME /data
    ```

14. WORKDIR指定工作目录，格式为：

    `WORKDIR /path/to/workdir`

    切换目录指令，类似于cd命令，写在该指令后的RUN，CMD以及ENTRYPOINT指令都将该目录作为当前目录，并执行相应的命令。

> Dockerfile官方文档：https://docs.docker.com/engine/reference/builder/#dockerfile-reference
>
> Dockerfile最佳实践：https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/#build-cache