### 提醒：滥用可能导致账户被删除！！！ 

将本项目fork或者上传至自己仓库修改`Deploy to Heroku`按键指向地址为自己仓库地址

[![](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy?template=https://github.com/louyour/ngix-fixed.git)

### heroku上部署v2ray

本项目只支持部署vless+ws+tls 或 vmess+ws+tls单协议节点，支持跳转伪装网页，伪装网页固定为3D元素周期表。

path路径自动设置为：/自定义UUID码-vless 或 /自定义UUID码-vmess


### 代理协议：vless+ws+tls 或 vmess+ws+tls
* 服务器地址：自选ip（如：icook.tw）或者：应用程序名.herokuapp.com
* 端口：443
* 默认UUID：自定义UUID码 
* 加密：none
* 传输协议：ws
* 伪装类型：none
* 伪装host：****.workers.dev(CF Workers反代地址)或者：应用程序名.herokuapp.com
* SNI地址：****.workers.dev(CF Workers反代地址)或者：应用程序名.herokuapp.com
* path路径：/自定义UUID码-vless 或 /自定义UUID码-vmess    (注意：前有斜杠/)
* vmess额外id（alterid）：0
* 底层传输安全：tls
* 跳过证书验证：false

### CloudFlare Workers反代代码
```js
addEventListener(
    "fetch",event => {
        let url=new URL(event.request.url);
        url.hostname="appname.herokuapp.com";
        let request=new Request(url,event.request);
        event. respondWith(
            fetch(request)
        )
    }
)
```
<summary>CloudFlare Workers单双日轮换反代代码</summary>

```js
const SingleDay = 'app0.herokuapp.com'
const DoubleDay = 'app1.herokuapp.com'
addEventListener(
    "fetch",event => {
    
        let nd = new Date();
        if (nd.getDate()%2) {
            host = SingleDay
        } else {
            host = DoubleDay
        }
        
        let url=new URL(event.request.url);
        url.hostname=host;
        let request=new Request(url,event.request);
        event. respondWith(
            fetch(request)
        )
    }
)
```
</details>
