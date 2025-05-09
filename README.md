# go-chatgpt-api

# 由于OAI无节制的降智，此项目归档。

# 此为个人维护的魔改版，相比原版，有以下改动/区别
Docker image: maxduke/go-chatgpt-api:latest

## 20250210
- [imitate]Add support for o3-mini
- **OAI降智太严重了，本人已经退订Plus，后期随时停止更新**

## 20241206
- [imitate]Add support for o1 && drop support for o1-preview

## 20241021
- Remove unused WSS code
- Update deps.

## 20240913
- [imitate]Add support for o1-preview & o1-mini

## 20240719
- [imitate]Add support for gpt-4o-mini
- [imitate]Drop support for gpt-3.5(text-davinci-002-render-sha)
- [imitate]*Plan to remove this endpoint in the future, recommend to use https://github.com/xqdoo00o/ChatGPT-to-API*

## 20240626
- Adjust default UA
- Test TurnstileToken generation (https://github.com/xqdoo00o/ChatGPT-to-API/commit/2cc5968fc70073c095d157fe8a9b5a2d66917eb6)
- Add new env variable
  - PROCESS_TURNSTILE (set to "true" to enable turnstile token generation)

## 20240612
- remove unused cookie
- add error log for checkRequire

## 20240527
- 尝试修复autoContiune, 增加环境变量
  - AUTO_CONTINUE - 默认 false

## 20240524
- 增加环境变量
  - POW_RETRY_TIMES - POW难度太高时，尝试重新获取POW种子的次数，默认0
  - POW_MAX_DIFFICULTY - POW最高难度设定，高于次难度将重试获取POW种子，默认"000032"

## 20240523
- 调整POW算法
- 增加环境变量
  - HARDWARE - 整数型，CPU核心数+屏幕分辨率高度+屏幕分辨率宽度。 不填则随机
  - POW_MAX_CALC_TIMES - 整数型，默认500000次。 CPU运算快的可以适当提高，减少403错误的概率

## 20240522
- 调整生成刷新 deviceID 逻辑
- 增加log: POW difficulty
- 更新POW算法 https://github.com/xqdoo00o/ChatGPT-to-API/commit/e69e3d8ab3de295eec7a73551fffdb3b9ce83b1b
- 在conversation payload中添加了一些新的字段，跟官网同步

## 20240520
- TEST: 尝试强制使用SSE，从而避免WSS的各种问题 （效果未知）
- 从request payload中移除arkoseToken （现在官网只在request header中有）

## 20240514
add gpt-4o support for imitate

## 20240507
调整backend域名  chat.openai.com => chatgpt.com

可能需要重新抓取har

## 20240506
调整POW以及更新部分接口域名

参照 https://github.com/xqdoo00o/ChatGPT-to-API/compare/2b6ea6e2208f11fbdf760ba23c1f704993901242...85aafb4cd9af1ed09e2120abc9bdae42bbacd271

## 20240503
后续计划移除imitate相关接口，有chat2api的需求的建议使用熊猫大佬的项目：

https://github.com/xqdoo00o/ChatGPT-to-API

## 20240501
调整chatrequirement以及pow算法

参照 https://github.com/xqdoo00o/ChatGPT-to-API/compare/d26911c672c9b0ce3c7928fec1109ff8539a34c1...89a038c3ca32bdbfdfcd2eff730aaaa9ff80ac7f
## 20240426
默认关闭 healthcheck, 如需要开启请配置新的环境变量
  - ENABLE_HEALTHCHECK
## 20240422 add POW
## 20240416 fix 403 error
添加新的环境变量
  - CLIENT_PROFILE
  - UA

没需求不要动
## 20240320 fix 403 error
## 20240314 imitate 重构
 - 更新依赖 https://github.com/xqdoo00o/funcaptcha
 - 移除环境变量 ENABLE_ARKOSE_3 , 程序将自动判断
 - 尝试重构 imitate， 参照 https://github.com/xqdoo00o/ChatGPT-to-API
## 20240206 imitate 支持 WSS
## 20240205 尝试支持官网改动之后的WSS协议 （imitate未支持）
参考 [32c0cf4b709ad3a7540f4a8ab0f7200c2ba92a9f](https://github.com/linweiyuan/go-chatgpt-api/commit/32c0cf4b709ad3a7540f4a8ab0f7200c2ba92a9f)

## 自动获取内部和更新的 Access token 和 PUID
配置环境变量
 - OPENAI_EMAIL
 - OPENAI_PASSWORD

或

 - OPENAI_REFRESH_TOKEN

自动生成和更新内部 Access token （用于imitate）和 PUID（仅PLUS账户）

推荐使用 OPENAI_REFRESH_TOKEN 方式， 使用邮箱和用户名的方式能否成功取决于抓取的har登陆时能否不出码

## 如何使用内部的 Access token ？
使用环境变量
 - IMITATE_API_KEY 虚拟一个api key， 当client发送的api key匹配时， 使用内部的 access token 转 API

集成最新 [funcaptcha](https://github.com/xqdoo00o/funcaptcha) 支持harPool, 映射目录 /app/harPool

[har获取方式](https://github.com/xqdoo00o/ChatGPT-to-API/blob/master/README_ZH.md#har%E6%96%87%E4%BB%B6%E6%B1%A0)

## ~~如何为3.5开启 ARKOSE TOKEN ？~~
~~使用环境变量~~
 - ~~ENABLE_ARKOSE_3=true~~
---

<details>
<summary>原版 README.md</summary>

## 一个尝试绕过 `Cloudflare` 来使用 `ChatGPT` 接口的程序

由于本人工作性质发生变化，每天通勤来回 4 小时以上 + 白天全程内网开发接触不到自己的代码，没时间继续维护，**已弃坑**，请换用其它还活着的项目

<details>
或者有没有老板赏识的可以介绍份好工作，那么就可以在完成自己的工作任务后摸鱼继续研究，联系方式：

![](https://linweiyuan.github.io/about/mmqrcode.png)
</details>

---

# 以下文档内容已过期，不一定支持（2023-10-24）

### 支持接口

- https://chat.openai.com/auth/login 登录返回 `accessToken`（谷歌和微软账号暂不支持登录，但可正常使用其他接口）
- 模型和插件查询
- `GPT-3.5` 和 `GPT-4` 对话增删改查及分享
- https://platform.openai.com/playground 登录返回 `apiKey`
- `apiKey` 余额查询
- 等等 ...
- 支持 `ChatGPT` 转 `API`，接口 `/imitate/v1/chat/completions`，利用 `accessToken` 模拟 `apiKey`，实现伪免费使用 `API`，从而支持集成仅支持 `apiKey` 调用的第三方客户端项目，分享一个好用的脚本测试 `web-to-api` (https://github.com/linweiyuan/go-chatgpt-api/issues/251)

```python
import openai

openai.api_key = "这里填 access token，不是 api key"
openai.api_base = "http://127.0.0.1:8080/imitate/v1"

while True:
    text = input("请输入问题：")
    response = openai.ChatCompletion.create(
        model='gpt-3.5-turbo',
        messages=[
            {'role': 'user', 'content': text},
        ],
        stream=True
    )

    for chunk in response:
        print(chunk.choices[0].delta.get("content", ""), end="", flush=True)
    print("\n")
```

范例（URL 和参数基本保持着和官网一致，部分接口有些许改动），部分例子，不是全部，**理论上**全部基于文本传输的接口都支持

https://github.com/linweiyuan/go-chatgpt-api/tree/main/example

---

### 使用的过程中遇到问题应该如何解决

汇总贴：https://github.com/linweiyuan/go-chatgpt-api/issues/74

如果有疑问而不是什么程序出错其实可以在 [Discussions](https://github.com/linweiyuan/go-chatgpt-api/discussions) 里发而不是新增 Issue

群聊：https://github.com/linweiyuan/go-chatgpt-api/discussions/197

再说一遍，不要来 `Issues` 提你的疑问（再提不回复直接关闭），有讨论区，有群，不要提脑残问题，反面教材：https://github.com/linweiyuan/go-chatgpt-api/issues/255

---

### 配置

如需设置代理，可以设置环境变量 `PROXY`，比如 `PROXY=http://127.0.0.1:20171` 或者 `PROXY=socks5://127.0.0.1:20170`，注释掉或者留空则不启用

如果代理需账号密码验证，则 `http://username:password@ip:port` 或者 `socks5://username:password@ip:port`

如需配合 `warp` 使用：`PROXY=socks5://chatgpt-proxy-server-warp:65535`，因为需要设置 `warp` 的场景已经默认可以直接访问 `ChatGPT` 官网，因此共用一个变量不冲突（国内 `VPS` 不在讨论范围内，请自行配置网络环境，`warp` 服务在魔法环境下才能正常工作）

家庭网络无需跑 `warp` 服务，跑了也没用，会报错，仅在服务器需要

`CONTINUE_SIGNAL=1`，开启 `/imitate` 接口自动继续会话功能，留空关闭，默认关闭

---

`GPT-4` 相关模型目前需要验证 `arkose_token`，社区已经有很多解决方案，请自行查找，其中一个能用的：https://github.com/linweiyuan/go-chatgpt-api/issues/252

参考配置视频（拉到文章最下面点开视频，需要自己有一定的动手能力，根据你的环境不同自行微调配置）：[如何生成 GPT-4 arkose_token](https://linweiyuan.github.io/2023/06/24/%E5%A6%82%E4%BD%95%E7%94%9F%E6%88%90-GPT-4-arkose-token.html)

---

根据你的网络环境不同，可以展开查看对应配置，下面例子是基本参数，更多参数查看 [compose.yaml](https://github.com/linweiyuan/go-chatgpt-api/blob/main/compose.yaml)

<details>

<summary>直接利用现成的服务</summary>

服务器不定时维护，不保证高可用，利用这些服务导致的账号安全问题，与本项目无关

- https://go-chatgpt-api.linweiyuan.com

</details>

<details>

<summary>网络在直连或者通过代理的情况下可以正常访问 ChatGPT</summary>

```yaml
services:
  go-chatgpt-api:
    container_name: go-chatgpt-api
    image: linweiyuan/go-chatgpt-api
    ports:
      - 8080:8080
    environment:
      - TZ=Asia/Shanghai
    restart: unless-stopped
```

</details>

<details>

<summary>服务器无法正常访问 ChatGPT</summary>

```yaml
services:
  go-chatgpt-api:
    container_name: go-chatgpt-api
    image: linweiyuan/go-chatgpt-api
    ports:
      - 8080:8080
    environment:
      - TZ=Asia/Shanghai
      - PROXY=socks5://chatgpt-proxy-server-warp:65535
    depends_on:
      - chatgpt-proxy-server-warp
    restart: unless-stopped

  chatgpt-proxy-server-warp:
    container_name: chatgpt-proxy-server-warp
    image: linweiyuan/chatgpt-proxy-server-warp
    restart: unless-stopped
```

</details>

---

目前 `warp` 容器检测到流量超过 1G 会自动重启，如果你知道什么是 `teams-enroll-token` （不知道就跳过），可以通过环境变量 `TEAMS_ENROLL_TOKEN` 设置它的值，然后利用这条命令来检查是否生效

`docker-compose exec chatgpt-proxy-server-warp warp-cli --accept-tos account | awk 'NR==1'`

```
Account type: Free （没有生效）

Account type: Team （设置正常）
```

---

### Render部署

点击下面的按钮一键部署，缺点是免费版本冷启动比较慢

[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy?repo=https://github.com/linweiyuan/go-chatgpt-api)

---

### 如何集成其他第三方客户端（下面的内容不一定是最新，有问题请去各自项目查看）

- [moeakwak/chatgpt-web-share](https://github.com/moeakwak/chatgpt-web-share)

环境变量

```
CHATGPT_BASE_URL=http://go-chatgpt-api:8080/chatgpt/backend-api/
```

- [lss233/chatgpt-mirai-qq-bot](https://github.com/lss233/chatgpt-mirai-qq-bot)

`config.cfg`

```
[openai]
browserless_endpoint = "http://go-chatgpt-api:8080/chatgpt/backend-api/"
```

- [Kerwin1202/chatgpt-web](https://github.com/Kerwin1202/chatgpt-web) | [Chanzhaoyu/chatgpt-web](https://github.com/Chanzhaoyu/chatgpt-web)

环境变量

```
API_REVERSE_PROXY=http://go-chatgpt-api:8080/chatgpt/backend-api/conversation
```

- [pengzhile/pandora](https://github.com/pengzhile/pandora)（不完全兼容）

环境变量

```
CHATGPT_API_PREFIX=http://go-chatgpt-api:8080
```

---

- [1130600015/feishu-chatgpt](https://github.com/1130600015/feishu-chatgpt)

`application.yaml`

```yaml
proxy:
  url: http://go-chatgpt-api:8080
```

---

- [Yidadaa/ChatGPT-Next-Web](https://github.com/Yidadaa/ChatGPT-Next-Web)

环境变量

```
BASE_URL=http://go-chatgpt-api:8080/imitate
```

---

### 相关博客（程序更新很多次，文章的内容可能和现在的不一样，仅供参考）：[ChatGPT](https://linweiyuan.github.io/categories/ChatGPT/)

- [如何生成 GPT-4 arkose_token](https://linweiyuan.github.io/2023/06/24/%E5%A6%82%E4%BD%95%E7%94%9F%E6%88%90-GPT-4-arkose-token.html)
- [利用 HTTP Client 来调试 go-chatgpt-api](https://linweiyuan.github.io/2023/06/18/%E5%88%A9%E7%94%A8-HTTP-Client-%E6%9D%A5%E8%B0%83%E8%AF%95-go-chatgpt-api.html)
- [一种解决 ChatGPT Access denied 的方法](https://linweiyuan.github.io/2023/04/15/%E4%B8%80%E7%A7%8D%E8%A7%A3%E5%86%B3-ChatGPT-Access-denied-%E7%9A%84%E6%96%B9%E6%B3%95.html)
- [ChatGPT 如何自建代理](https://linweiyuan.github.io/2023/04/08/ChatGPT-%E5%A6%82%E4%BD%95%E8%87%AA%E5%BB%BA%E4%BB%A3%E7%90%86.html)
- [一种取巧的方式绕过 Cloudflare v2 验证](https://linweiyuan.github.io/2023/03/14/%E4%B8%80%E7%A7%8D%E5%8F%96%E5%B7%A7%E7%9A%84%E6%96%B9%E5%BC%8F%E7%BB%95%E8%BF%87-Cloudflare-v2-%E9%AA%8C%E8%AF%81.html)

---

### 最后感谢各位同学

<a href="https://github.com/linweiyuan/go-chatgpt-api/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=linweiyuan/go-chatgpt-api"  alt=""/>
</a>

---

![](https://linweiyuan.github.io/about/mm_reward_qrcode.png)
