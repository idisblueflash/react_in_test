# webpack的dev模式下跨站
webpack的dev跑起来，但是需要调用其他api实现功能，如何跨站？

```
+++ b/app/src/components/LoginPage.js
@@ -28,7 +28,7 @@ var LoginPage = React.createClass({
   handleCheckPhoneNumber: function(testId){
     var phoneNumberValid = validator.isMobilePhone(this.state.phoneNumber, 'zh-CN');
     if(phoneNumberValid){
-      var url = "localhost:3000/user/exist_check";
+      var url = "/api/user/exist_check";
       $.ajax({
         url: url,
         method: 'POST',
```

```
+++ b/app/src/server/server.js
@@ -4,7 +4,9 @@ var mobiles = ['13552987637'];
 
 var server = http.createServer(function (req, res) {
   console.log(req.url);
-  if ('/user/exist_check' == req.url) {
+  res.setHeader('Content-Type', 'text/json');
+
+  if ('/api/user/exist_check' == req.url) {
     switch (req.method) {
       case 'POST':
         exist_check(req, res);
```

```
+++ b/webpack.config.js
@@ -22,6 +22,9 @@ var config = {
             loader: 'style!css'
         }],
         noParse: [pathToReact]
+    },
+    devServer: {
+        proxy: { '/api/*' : 'http://localhost:3000' }
     }
 };
```
       