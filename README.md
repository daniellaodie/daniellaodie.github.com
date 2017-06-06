eric--.github.com
=================

## use
use for hexo

## test ssh git
ssh -vT git@github.com

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
* 设置ssh链接
```
	hexo ssh
```