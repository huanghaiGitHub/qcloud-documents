1. 登录 [云函数控制台](https://console.cloud.tencent.com/scf/list?rid=1)，进入**函数服务**页面。
2. 选择**广州**地域，单击**新建**，进入新建函数页面。
3. 填写以下参数信息，单击**下一步**。
 - 创建方式：选择 “空白函数”。
 - 函数名称：命名为 hello-world。
 - 运行环境：选择 Python2.7。
4. 保持默认配置，单击**完成**，完成函数的创建。如下图所示： 
![](https://main.qcloudimg.com/raw/cf9ef2a855d259d8cc1af773890535b7.png)
 - “执行方法” 的 “index.main_handler” 参数值表示 SCF 控制台会将此段代码自动保存为 `index.py` 文件，并将该文件压缩和上传至 SCF 平台，用于创建云函数。
 - 示例代码中的 `main_handler` 为入口函数，主要有以下两个入参：
    - `event`参数：可以获取触发源的消息。
    - `context`参数：可以获取本函数的环境及配置信息。

 >? 函数创建完成后，您可以在**函数配置**里查看函数配置等信息，也可以在**函数代码**中在线编辑代码。

