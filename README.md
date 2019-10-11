eric--.github.com
=================

## use
use for hexo

## bak for hexo source   
* 博客的源文件，用于电脑变更的迁移
* eric--.github.io 这个库是 hexo deploy 的目标
 
## 迁移步骤
* copy source
```
git clone https://github.com/Eric--/eric--.github.com.git hexo
```
* 安装依赖
```
npm install -g hexo-cli && npm install
```
* 下载主题（主题内容太大，所以不备份，需要主动下载）
```
cd  hexo --进入目录下载主题
git clone https://github.com/iissnan/hexo-theme-next themes/next
```
* 配置主题（因为主题文件重新下载，所以要重新配置 themes目录下的 _config.yml）
```
	scheme: Pisces
	local_search:
		enable: true
```
* 设置git hexo ssh链接（如果新机器有，直接用公钥就好）
```
	git config --global user.email "steven@isteven.info"
	git config --global user.name "steven"
	ssh-keygen -t rsa -C "steven@isteven.info"
	.ssh 下生成两个rsa公钥秘钥对文件，id_rsa/id_rsa.pub
	将id_rsa.pub内容copy到github上
	ssh -vT git@github.com  验证
```