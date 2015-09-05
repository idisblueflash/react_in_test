# 在localhost:9876找不到logo.png
```
05 09 2015 10:47:53.724:WARN [web-server]: 404: /imgs/logo.png
```

### 分析
目录在测试服务器下没有配置。

### 解法
将png包含到webpack内

安装url-loader

    npm install url-loader --save-dev
    
配置karma.conf.js，添加 ,{test: /\.(png|jpg)$}/, loader:'url?limit=25000'}

```
   webpack:{
        module: {
            preLoaders: [
                {test: /\.js$/, loader: 'babel'},
                {test: /\.(png|jpg)$}/, loader:'url?limit=25000'}
            ]
        },
        watch: true
    }, 
```    

  


