使用anywhere可以快速建立一个web站点

示例

在网站目录下放一个anywhere.cmd，全局安装anywhere，然后将anywhere.cmd拷贝到网站目录下。

package.json示例

```
{
  "name": "es6tutorial",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "directories": {
    "doc": "docs"
  },
  "scripts": {
    "test": "start index.html"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/ruanyf/es6tutorial.git"
  },
  "devDependencies": {
    "anywhere": "1.4.0"
  },
  "author": "ruanyifeng",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/ruanyf/es6tutorial/issues"
  },
  "homepage": "https://github.com/ruanyf/es6tutorial#readme"
}
```

双击anywhere.cmd启动站点服务