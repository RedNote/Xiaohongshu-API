# Xiaohongshu API — 小红书数据采集 & 互动接口

> **Rnote API** — 专业的小红书 APP 数据 API 服务平台，22+ 端点覆盖笔记、用户、搜索、商品、话题、互动全场景。
>
> 一手资源，独家 APP 端逆向，全网最稳定的小红书代采接口。市面上很多代采服务商都是二次封装我们的服务。

<p align="center">
  <a href="https://rnote.dev/">官网</a> ·
  <a href="https://rnote.dev/docs/guide">API 文档</a> ·
  <a href="https://docs.rnote.dev/">在线调试</a> ·
  <a href="https://rnote.dev/pricing">定价</a> ·
  <a href="https://rnote.dev/dealer">经销商</a> ·
  <a href="https://rnote.dev/supplier">供应商</a> ·
  <a href="https://t.me/Evil_Geek">Telegram</a>
</p>

---

## 为什么选择我们

| 优势 | 说明 |
| --- | --- |
| **一手资源** | 独家 APP 端逆向，非二次转售，延迟低、稳定性高 |
| **22+ API 端点** | 笔记详情、评论、搜索、用户、商品、话题、互动操作一站覆盖 |
| **智能账号池** | 多账号自动轮换，内置风控检测与冷却机制，无需自行管理账号 |
| **按需计费** | 仅成功请求扣费（HTTP 2xx），失败请求零费用 |
| **实时接口** | 直连小红书 APP，数据实时返回，无缓存延迟 |
| **多语言 SDK** | 提供 cURL / Python / JavaScript / TypeScript / Java / Go / PHP 示例 |
| **在线调试** | 基于 Apifox 的在线调试环境，输入 API Key 即可在浏览器测试 |
| **经销商体系** | 成为经销商享永久折扣 + 邀请返利，灵活转余额给客户 |

---

## 接口总览

### 数据采集接口（Crawler）

| 接口 | 端 | 说明 |
| --- | --- | --- |
| 图文笔记详情 | APP | 获取图文笔记完整信息、图片列表、作者、互动数据 |
| 视频笔记详情 | APP | 获取视频笔记信息、播放地址、封面 |
| 首页推荐流 | APP | 获取个性化推荐 Feed 流内容 |
| 笔记评论列表 | APP | 分页获取笔记评论，支持按热度/时间排序 |
| 评论子回复列表 | APP | 获取评论的子回复，游标分页 |
| 用户信息 | APP | 获取用户昵称、头像、简介、粉丝数等 |
| 用户发布笔记 | APP | 分页获取用户已发布的笔记列表 |
| 用户收藏笔记 | APP | 分页获取用户收藏的笔记列表 |
| 搜索笔记 | APP | 关键词搜索笔记，支持排序/类型/时间筛选 |
| 搜索用户 | APP | 按关键词搜索用户 |
| 搜索图片 | APP | 按关键词搜索图片 |
| 搜索商品 | APP | 搜索小红书电商商品 |
| 搜索群聊 | APP | 搜索小红书群聊 |
| 商品详情 | APP | 获取商品完整信息 |
| 商品评价概览 | APP | 获取商品评价统计数据 |
| 商品评价列表 | APP | 分页获取商品评价 |
| 商品推荐 | APP | 获取相关推荐商品 |
| 话题详情 | APP | 获取话题/标签详情 |
| 话题笔记流 | APP | 获取话题下的笔记 Feed |
| 创作灵感 | APP | 获取创作者灵感推荐 |
| 热门灵感 | APP | 获取热门创作灵感 |

### 互动接口（Interaction）

| 接口 | 端 | 说明 |
| --- | --- | --- |
| 点赞笔记 | APP | 对指定笔记执行点赞操作，自动去重 |
| 收藏笔记 | APP | 收藏指定笔记，自动去重 |
| 关注用户 | APP | 关注指定用户，自动去重 |

> 更多接口持续开发中，也可联系我们定制开发。

---

## 快速开始

### 1. 注册账号

访问 [rnote.dev/auth/register](https://rnote.dev/auth/register) 免费注册，注册后在管理后台创建 API Key。

### 2. 调用接口

所有接口使用 `X-API-Key` Header 认证：

**cURL**
```bash
curl -X GET "https://rnote.dev/api/v1/crawler/note/image?note_id=NOTE_ID" \
  -H "X-API-Key: YOUR_API_KEY"
```

**Python**
```python
import requests

resp = requests.get(
    "https://rnote.dev/api/v1/crawler/note/image",
    params={"note_id": "NOTE_ID"},
    headers={"X-API-Key": "YOUR_API_KEY"},
)
print(resp.json())
```

**JavaScript**
```javascript
const resp = await fetch(
  "https://rnote.dev/api/v1/crawler/note/image?note_id=NOTE_ID",
  { headers: { "X-API-Key": "YOUR_API_KEY" } }
);
const data = await resp.json();
console.log(data);
```

### 3. 在线调试

我们提供基于 [Apifox 的在线调试环境](https://docs.rnote.dev/)，输入 API Key 即可在浏览器中直接测试所有接口，无需编写代码。

---

## 响应格式

**成功响应**
```json
{
  "success": true,
  "data": { ... },
  "device_id": "device_xxxxx"
}
```

**错误响应**
```json
{
  "success": false,
  "error": "错误信息",
  "device_id": "device_xxxxx"
}
```

### HTTP 状态码

| 状态码 | 含义 | 是否计费 |
| --- | --- | --- |
| `200` | 请求成功 | 计费 |
| `400` | 参数错误 | 不计费 |
| `401` | API Key 无效 | 不计费 |
| `402` | 余额不足 | 不计费 |
| `429` | 请求频率超限 | 不计费 |
| `5xx` | 服务端错误 | 不计费 |

---

## 计费说明

- **按需计费**：每次成功的 API 调用按固定单价扣费
- **仅成功扣费**：只有 HTTP 2xx 响应才扣费，所有失败请求（网络错误、服务端错误、参数错误、余额不足）均不扣费
- **透明定价**：无隐藏费用，无最低消费，管理后台实时查看余额和消费明细
- **充值方式**：联系管理员或通过经销商充值，余额即时到账

查看详细定价：[rnote.dev/pricing](https://rnote.dev/pricing)

---

## 核心特性

### 智能账号池
多账号自动轮换，单个账号触发风控自动冷却切换，无需手动管理。支持大陆版 / 海外版设备路由。

### 风控检测与自动恢复
- 频率限制自动检测与冷却
- 登录过期自动标记与设备切换
- 账号异常自动隔离
- 连续风控触发自动补充账号
- 风控设备自动解封

### 签名服务
APP 端实时签名，支持 `x-mini-sig`、`x-mini-gid`、`x-mini-mua`、`xy-common-params`、`xy-platform-info` 等全部签名参数，无需自行处理加密逻辑。

### 管理后台
- 用户管理 & API Key 管理
- 设备池状态监控
- 数据分析看板
- 计费明细与交易记录
- 工作流管理

---

## 合作模式

### 经销商合作
成为经销商享永久折扣 + 邀请返利，灵活为客户转余额。详情：[rnote.dev/dealer](https://rnote.dev/dealer)

### 供应商合作
拥有小红书账号资源？通过分成系统共享收益，长期稳定合作。详情：[rnote.dev/supplier](https://rnote.dev/supplier)

---

## 联系我们

- **Telegram**：[@Evil_Geek](https://t.me/Evil_Geek)（推荐，快速响应）
- **Email**：Support@rnote.dev

---

## 相关链接

| 链接 | 说明 |
| --- | --- |
| [rnote.dev](https://rnote.dev/) | 官网首页 |
| [rnote.dev/docs/guide](https://rnote.dev/docs/guide) | API 快速上手文档 |
| [docs.rnote.dev](https://docs.rnote.dev/) | Apifox 在线调试环境 |
| [rnote.dev/pricing](https://rnote.dev/pricing) | 定价页面 |
| [rnote.dev/status](https://rnote.dev/status) | 服务状态监控 |
| [rnote.dev/dealer](https://rnote.dev/dealer) | 经销商合作 |
| [rnote.dev/supplier](https://rnote.dev/supplier) | 供应商合作 |
| [rnote.dev/contact](https://rnote.dev/contact) | 联系我们 |

---

## 许可证

Apache License 2.0 — 详见 [LICENSE](LICENSE)

---

<!-- SEO Keywords -->
<!--
小红书API 小红书爬虫 小红书采集 小红书数据 小红书接口 小红书数据采集
小红书APP接口 小红书逆向 小红书签名 RedNote API Xiaohongshu API
小红书笔记详情 小红书用户信息 小红书搜索 小红书评论 小红书商品
小红书点赞 小红书收藏 小红书关注 小红书互动 小红书自动化
小红书账号池 小红书风控 小红书代采 小红书数据服务 小红书批量采集
小红书主页 小红书作者页 小红书作品列表 小红书话题 小红书标签
小红书电商 小红书商品详情 小红书商品搜索 小红书商品评价
小红书视频 小红书图文 小红书推荐流 小红书Feed
批量发笔记 批量点赞 批量关注 批量评论 批量收藏
x-mini-sig x-mini-gid x-mini-mua x-mini-s1 xy-common-params xy-platform-info
x-legacy-smid x-legacy-did x-legacy-fid x-legacy-sid main_hmac
App Shield 算法 x-s x-s-common Web签名
Rnote API 小红书数据平台 RESTful API 按需计费 实时数据
小红书SDK 小红书Python 小红书JavaScript 小红书Java 小红书Go
RedNote data scraping RedNote crawler RedNote scraper Xiaohongshu scraper
Xiaohongshu data collection Xiaohongshu note Xiaohongshu user Xiaohongshu search
Little Red Book API social media API China social media data
-->
