# hexo

## 更换电脑之后的配置过程
``` bash
git clone git@github.com:rui-noworry/hexo.git

```
### 全局安装hexo-cli
``` bash
npm install -g hexo-cli

```
### 安装node包
``` bash
npm install

```
### 运行项目
``` bash
hexo g
hexo s

预览页面的时候会发现空白的情况，需要重新下载主题：
 git clone https://github.com/iissnan/hexo-theme-next themes/next


没问题之后就发布
hexo d

```