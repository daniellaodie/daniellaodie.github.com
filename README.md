eric--.github.com
=================

## use
use for hexo

## bak for hexo source   
 博客的源文件，用于电脑变更的迁移
 
## 迁移步骤
* copy source
```
git clone combak
```
* 安装依赖
```
npm install -g hexo-cli && npm install
```
* 下载主题
```
download theme git clone https://github.com/iissnan/hexo-theme-next themes/next
```
* 配置主题
```
	scheme: Pisces
	local_search:
		enable: true
```
* 设置git hexo ssh链接
```
	git config --global user.email "steven@isteven.info"
	git config --global user.name "steven"
	ssh-keygen -t rsa -C "steven@isteven.info"
	.ssh 下生成两个rsa公钥秘钥对文件，id_rsa/id_rsa.pub
	将id_rsa.pub内容copy到github上
	ssh -vT git@github.com  验证
```