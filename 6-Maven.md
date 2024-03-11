# Maven

## 查看自己安装的maven的版本

> 首先window+R输入[cmd](https://so.csdn.net/so/search?q=cmd&spm=1001.2101.3001.7020)进入命令符。
>
> mvn ：查看环境是否有问题
>
> ![image-20230507103442089](C:\Users\16055\AppData\Roaming\Typora\typora-user-images\image-20230507103442089.png)



> 其次再输入mvn -vesion就可以查看当前版本了
>
> ![image-20230507103540080](C:\Users\16055\AppData\Roaming\Typora\typora-user-images\image-20230507103540080.png)



## 在idea上查看项目使用的maven

> 本地仓库是远程仓库的一个子集，当你构建Maven项目的时候首先会从本地仓库中查找资源
>
> 如果没有，则会从远程仓库中下载到本地仓库（下次使用会从本地仓库中查找资源）
>
> 如果本地远程仓库也没有，那么Maven在构建的时候会报错，这种情况可能是有些jar包的新版本没有在Maven仓库中及时更新
>
> 下图上的User settings file就是您的manven仓库的路径地址 
>
> Local repository ：就是本地仓库

> ![image-20230507103821738](C:\Users\16055\AppData\Roaming\Typora\typora-user-images\image-20230507103821738.png)

## **自定义修改仓库的存储位置：**

可改变默认的 .m2 目录下的默认本地存储库文件夹
通过修改${user.home}/.m2/settings.xml 配置本地仓库路径 ，没有settings这个xml文件就新建，或者如下复制个；具体看图：

这是修改后的本地仓库

![image-20230507104554011](C:\Users\16055\AppData\Roaming\Typora\typora-user-images\image-20230507104554011.png)

![image-20230507104807505](C:\Users\16055\AppData\Roaming\Typora\typora-user-images\image-20230507104807505.png)