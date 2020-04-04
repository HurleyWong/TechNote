## Google Colab断线自动重连

因为Google Colab是Google提供给广大开发者的免费的云服务器，所以功能肯定也是相当有限的。会经常出现训练一半，自动断开连接问题。

那么，可以通过在网页控制台（Console）中输入以下命令回车即可：

```javascript
function ClickConnect(){
    console.log("Working"); 
    document.querySelector("colab-toolbar-button#connect").click() 
}
setInterval(ClickConnect,60000)
```

