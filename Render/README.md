<div style="text-align: center"></div>
  <p align="center">
  <img src="https://github.com/dqzboy/Docker-Proxy/assets/42825450/c187d66f-152e-4172-8268-e54bd77d48bb" width="230px" height="200px">
      <br>
      <i>使用 Render 快速部署我们的Docker镜像加速服务.</i>
  </p>
</div>

---

[Telegram Group](https://t.me/+ghs_XDp1vwxkMGU9) 

<details>
<summary>点击此处加入微信交流群</summary>
<div align="center">
<img src="https://raw.githubusercontent.com/dqzboy/Blog-Image/main/TEG/dqzboy-it.png" width="400px">
</div>
</details>

---


## 📦 部署
**1. 登入 [Render](https://dashboard.render.com)**

**2. 创建我们的服务**
<table>
    <tr>
        <td width="50%" align="center"><img src="https://github.com/dqzboy/Blog-Image/assets/42825450/7a16000a-6514-4cc9-892c-9f0a9746d1b2?raw=true"></td>
    </tr>
</table>

<table>
    <tr>
        <td width="50%" align="center"><img src="https://github.com/dqzboy/Docker-Proxy/assets/42825450/e5bb8e70-2bba-4b3f-a29f-fcf56ac2b82a?raw=true"></td>
    </tr>
</table>

**3. 选择以docker容器的方式部署，输入下面任一镜像地址**
  
| 镜像 | 平台 |
|-------|---------------|
| dqzboy/hub:latest   | docker hub
| dqzboy/gcr:latest      | Google Container Registry
| dqzboy/ghcr:latest     | GitHub Container Registry
| dqzboy/k8sgcr:latest  | Kubernetes Container Registry
| dqzboy/quay:latest     | Quay Container Registry

<table>
    <tr>
        <td width="50%" align="center"><img src="https://github.com/dqzboy/Docker-Proxy/assets/42825450/3f84c551-bef4-4e00-a3b4-b85e34a7eb7e?raw=true"></td>
    </tr>
</table>

<table>
    <tr>
        <td width="50%" align="center"><img src="https://github.com/dqzboy/Docker-Proxy/assets/42825450/907ba8da-9c1d-4cfb-9951-b843fabe47a9?raw=true"></td>
    </tr>
</table>

**4. 实例类型选择免费即可(免费实例需要保活,可使用 [uptime-kuma](https://uptime.kuma.pet/) 或 [D监控](https://www.dnspod.cn/Products/Monitor) 实现)**

<table>
    <tr>
        <td width="50%" align="center"><img src="https://github.com/dqzboy/Blog-Image/assets/42825450/c0a166c9-9d06-472e-a4cd-0d16fa3eeb83?raw=true"></td>
    </tr>
</table>

**5. 环境变量不用添加，直接选择创建即可**
<table>
    <tr>
        <td width="50%" align="center"><img src="https://github.com/dqzboy/Blog-Image/assets/42825450/e760d9c3-b6f4-4a5e-81ce-64c8017c70fc?raw=true"></td>
    </tr>
</table>

**6. 等待服务运行完成之后，使用分配的外网域名即可愉快的使用了**
<table>
    <tr>
        <td width="50%" align="center"><img src="https://github.com/dqzboy/Docker-Proxy/assets/42825450/95793a23-5831-4565-9c23-03130b81e8be?raw=true"></td>
    </tr>
</table>

## ✨ 使用

**1. 改Docker的daemon.json配置，配置你Render服务地址。修改后重启docker**
```shell
~]# vim /etc/docker/daemon.json
{
    "registry-mirrors": [ "https://your_render_url" ],
    "log-opts": {
      "max-size": "100m",
      "max-file": "5"
    }
}
```
**2. 使用Render服务地址替换官方的 Registry 地址拉取镜像**
```shell
# docker hub Registry
## 源：redis:latest
## 替换
docker pull your_render_url/library/redis:latest
```

> **说明**：如果上面配置了docker的daemon.json，那么拉取镜像的时候就不需要在镜像前面加Render_URL了。【只针对Docker生效】

**3. 拉取速度测试，效果还是可以的，主要是免费**
![image](https://github.com/dqzboy/Blog-Image/assets/42825450/06ad14d4-cb0f-4924-ab41-5c3f001261a2)

**4. 前缀替换的 Registry 的参考**

| 源站 | 替换为 | 平台 |
|-------|---------------|----------|
| docker.io   | your_render_url   |  docker hub 
| gcr.io      | your_render_url   |  Google Container Registry
| ghcr.io     | your_render_url  |  GitHub Container Registry
| k8s.gcr.io     | your_render_url  | Kubernetes Container Registry
| quay.io     | your_render_url  | Quay Container Registry

## ⚠️ 注意
**1.** 免费实例如果15分钟内未收到入站流量，Render会关闭实例的网络服务。Render 会在下次收到处理请求时重新启动该服务。

**2.** Render每月为每个用户和团队提供 750 小时的免费实例时间：
   - 免费网络服务在运行期间会消耗这些时间（停止服务不要消耗免费实例
   - 小时数）。
   - 如果您在某个月内用完了所有免费实例小时数，Render将暂停您的所有免费网络服务，直到下个月开始。
   - 每个月开始时，您的免费实例小时数将重置为 750 小时（剩余小时数不会结转）。

**3.** 最好自己个人使用或者小团队使用，如果你的服务使用人多了，Render照样会把你的服务给删除掉，并且没有任何提醒！