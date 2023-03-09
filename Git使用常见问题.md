# 常见问题汇总

Q1:如何解决error: failed to push some refs to <https://gitee.com/>

**问题描述：**

> 在 git 执行命令git push origin master时，报错error: failed to push some refs to <https://gitee.com/>
根本原因是远程仓库和本地仓库内容不同，将远程仓库中不同的内容pull到本地，就好了。
比如，我是新建了一个远程仓库，准备把本地内容上传时，忘记把远程仓库的redme.md文件同步出错的。

**解决办法：**

```shell
git pull 远程库别名或远程库地址链接 分支名（通常是master）

# 将redme.md文件同步到本地，然后再次执行git push就好了
```
