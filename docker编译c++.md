


#docker开发环境使用

##windows使用dokcer作为编译容器+开发环境（目前主要是cmake+GCC）
---

1. 在windows或者macOS安装docker

2. 自行编写dockerfile构建带有GCC+cmake的镜像或者dockerhub上直接找相应可用镜像

我这里有现成可用的
`docker pull nercury/cmake-cpp:gcc-4.8`

3. 在容器中编译代码，本地就可以直接得到可执行文件

   * 跟容器可以交互，相当于本地起了一个linxu服务器

`docker run -it --name cmake -v C:\Users\Administrator\Desktop\lego:/opt -w /opt nercury/cmake-cpp:gcc-4.8 /bin/bash`

-v 参数后面是  源码位置：容器目录（把宿主机的目录挂载到容器中，在容器中直接访问宿主机的源码）


* 不跟容器交互，把容器当作编译机，直接到源码目录拿编译结果

`docker run  --name cmake  -v C:\Users\Administrator\Desktop\lego:/opt -w=/opt nercury/cmake-cpp:gcc-6.1  /bin/bash -c "mkdir build && cd build && cmake .. && make"`

docker容器化可以方便的在windows上开发，直接验证编译结果，不需要推送不确定代码到分支再到linux下编译


##linux 下搭建编译环境 
---

c++代码有时需要特定版本编译，这样每次都得更新GCC版本（GCC太难管理了）
有一种很好的方式管理编译，那就是利用docker，原理上跟windows上一致

1. 安装docker

2. 拉取合适cmake和GCC版本镜像 

`docker pull nercury/cmake-cpp:gcc-4.8`

3. 利用docker编译代码

```
docker run -it --name cmake -v ~/lego:/opt -w /opt nercury/cmake-cpp:gcc-4.8 /bin/bash
mkdir build && cd build && cmake ..
make
```
4. ok，去build看编译好的可执行文件吧

