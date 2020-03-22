## Postman发送JSON格式的POST请求

1. 设置Header：

    Content-Type application/json

2. 设置Body：

    ![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Untitled.png)

    在body中设置选项为raw，然后以下的格式发送

    ```json
    {
     	"code": 0,
     	"message": success,
     	"data" : {}
     }
    ```