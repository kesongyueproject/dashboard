部署文档

---

### 1、前端部署

1. 安装微信小程序 IDE
2. 克隆仓库：[https://github.com/kesongyueproject/EarnSpareMoney](https://github.com/kesongyueproject/EarnSpareMoney)
3. 使用 IDE 创建项目，项目文件夹指向克隆得到的项目文件夹

---

### 2、后端部署

##### 2.1 配置

​	主要为Node.js。

- Node.js

  * 首先在官网下载对应你系统的Node.js版本，解压安装后打开命令提示符窗口，输入：

  ```
  	node -v
  	npm -v
  ```

  * 检查其是否安装成功。之后配置npm安装的全局模块所在的路径，以及缓存cache的路径，打开命令行输入以下指令：

  ```
  	npm config set prefix "D:\Develop\nodejs\node_global"
  	npm config set cache "D:\Develop\nodejs\node_cache"
  ```

  ​	（两条指令最后边为其模块所在的绝对路径）

  ​	 ![](/images/configuration1.png)

  * 进入环境变量对话框，在【系统变量】下新建【NODE_PATH】，输入【D:\Develop\nodejs\node_global\node_modules】，将【用户变量】下的【Path】修改为【D:\Develop\nodejs\node_global】

    ![](/images/configuration2.png)

    ![](/images/configuration3.png)





##### 2.2 运行

​	拉取github仓库里的代码并配置好相关环境后，在项目后端代码文件夹的根目录运行指令：npm start即可运行服务端。