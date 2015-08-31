# 找不到node文件或目录

```
npm init
env: node: No such file or directory
``` 
### 解法1：安装node（参考环境要求）

### 解法2: 用nvm切换node版本

得到当前支持的node版本，输入：
    
    mvn ls
    
（以下结果根据环境不同会有变化）：

````
iojs-v3.0.0
       v0.10.32
       v0.10.34
        v0.12.2
        v0.12.7
stable -> 0.12 (-> v0.12.7) (default)
````
使用最新node版本，输入：

    nvm use v0.12
    
成功切换到v9.12.7

    Now using node v0.12.7