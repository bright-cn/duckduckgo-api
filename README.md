# DuckDuckGo 搜索爬取器

[![Promo](https://media.www.bright.cn/2025/08/SERP-API-50-off-GitHub-banner_1389_166.png)](https://www.bright.cn/products/serp-api/duckduckgo-search)

本仓库提供两种从 DuckDuckGo 搜索结果页（SERPs）提取数据的方案：

- 免费 DuckDuckGo 爬虫：用于小规模抓取 DuckDuckGo 搜索结果的工具
- 企业级 DuckDuckGo SERP API：适用于高并发、实时数据提取的可扩展生产级方案（隶属于[Bright Data 的 SERP Scraper API](https://www.bright.cn/products/serp-api)）

## 目录

- [免费 DuckDuckGo SERP 爬虫](#免费-duckduckgo-serp-爬虫)
  - [环境准备](#环境准备)
  - [快速开始指南](#快速开始指南)
  - [示例输出](#示例输出)
  - [限制](#限制)
- [DuckDuckGo SERP API](#duckduckgo-serp-api)
  - [主要优势](#主要优势)
  - [开始使用](#开始使用)
- [接入方式](#接入方式)
  - [直接 API 访问](#直接-api-访问)
  - [原生代理访问](#原生代理访问)
- [DuckDuckGo 搜索查询参数](#duckduckgo-搜索查询参数)
  - [本地化](#本地化)
  - [安全搜索设置（kp）](#安全搜索设置-kp)
  - [时间范围筛选（df）](#时间范围筛选-df)
  - [设备定向（brd_mobile）](#设备定向-brd_mobile)
  - [浏览器仿真（brd_browser）](#浏览器仿真-brd_browser)
- [实用示例](#实用示例)
- [支持与资源](#支持与资源)

## 免费 DuckDuckGo SERP 爬虫
该免费爬虫提供一种简单方式用于小规模收集搜索结果数据。若你仅需有限数据且不想管理代理或处理高并发，这是理想选择。

<img width="800" alt="free-duckduckgo-serp-scraper" src="https://github.com/bright-cn/duckduckgo-api/blob/main/images/428465443-0472593e-615c-4723-96e7-08f83cb0b477.png" />

### 环境准备

- Python 3.9+ – [下载 Python](https://www.python.org/downloads/)
- 依赖包：
- `selenium`（浏览器自动化）
- `webdriver-manager`（浏览器驱动管理）
- `beautifulsoup4`（HTML 解析）

安装命令：
```bash
pip install selenium webdriver-manager beautifulsoup4
```

> Web 抓取新手？
> 可先阅读我们的[Python 入门抓取指南](https://www.bright.cn/blog/how-tos/web-scraping-with-python)。随后参阅[在抓取中使用 Selenium](https://www.bright.cn/blog/how-tos/using-selenium-for-web-scraping)，若已熟悉 Selenium，可继续阅读高级的 [SeleniumBase 指南](https://www.bright.cn/blog/web-data/web-scraping-with-seleniumbase)。

### 快速开始指南

1. 打开 [duckduckgo-serp-scraper.py](https://github.com/triposat/DuckDuckGo-Search-Scraper/blob/main/duckduckgo-serp-scraper/duckduckgo-serp-scraper.py)。
2. 按需自定义搜索词：
```python
SEARCH_TERMS = [
ergonomic office chair,
coffee maker,
]
```
3. 运行脚本开始抓取。

### 示例输出
如下为爬虫输出预览：

<img width="800" alt="free-duckduckgo-serp-scraper-output" src="https://github.com/bright-cn/duckduckgo-api/blob/main/images/428465286-d6891a93-2b5f-4243-8a17-e2a037c91570.png" />

### 限制

尽管免费爬虫适合基础任务，但需注意以下限制：

- 频繁使用容易导致 IP 被封
- 请求量能力有限
- 易频繁触发 CAPTCHA
- 不适合生产环境

如需可扩展且稳定的方案，请参考下文的专用 API 👇

## DuckDuckGo SERP API

DuckDuckGo SERP API 是 Bright Data 全面 [SERP Scraper API](https://www.bright.cn/products/serp-api) 套件的一部分。它利用我们行业领先的 [DuckDuckGo 代理基础设施](https://www.bright.cn/solutions/duckduckgo-proxies)，仅用一次 API 调用即可获取实时 DuckDuckGo 搜索结果。

### 主要优势

- 全球精确度：可按任意地区定制结果
- 成功即付费：仅为成功请求付费
- 实时数据：秒级获取最新结果
- 无限扩展：轻松应对高并发抓取
- 成本高效：无需昂贵自建基础设施
- 稳定可靠：先进防封技术保障一致结果
- 7x24 专家支持：随时获得协助

📌 先试后买：使用我们的 [SERP API 在线演示](https://www.bright.cn/products/serp-api/duckduckgo-search)。

<img width="800" alt="bright-data-serp-api-playground" src="https://github.com/bright-cn/duckduckgo-api/blob/main/images/428471522-fc60e165-e4db-41d2-93eb-2b6a01398353.png" />

### 开始使用

1. [创建 Bright Data 账户](https://www.bright.cn/)（新用户可获 $5 额度）
2. 生成你的[API 密钥](https://docs.www.bright.cn/general/account/api-token)
3. 按照[配置指南](https://github.com/triposat/DuckDuckGo-Search-Scraper/blob/main/setup-serp-api.md)集成 SERP API

## 接入方式

你可以通过以下两种方式将 DuckDuckGo SERP API 集成到你的工作流中：

### 直接 API 访问

直接请求 Bright Data 的 API 端点。

#### cURL 示例

```bash
curl https://api.www.bright.cn/request \
-H "Content-Type: application/json" \
-H "Authorization: Bearer API_TOKEN" \
-d '{
zone: "ZONE_NAME",
url: "https://duckduckgo.com/?q=budget+laptops+under+500+gbp&kl=uk-en&kad=en-gb&df=w",
format: "raw"
}'
```

#### Python 示例

```python
import requests

url = "https://api.www.bright.cn/request"

headers = {
Content-Type: "application/json",
Authorization: "Bearer API_TOKEN"
}

payload = {
zone: "ZONE_NAME",
url: "https://duckduckgo.com/?q=budget+laptops+under+500+gbp&kl=uk-en&kad=en-gb&df=w",
format: "raw",
}

response = requests.post(url, headers=headers, json=payload)

with open("duckduckgo-scraper-api-result.html", "w", encoding="utf-8") as file:
file.write(response.text)

print("Response saved!")
```

### 原生代理访问

通过代理路由直接访问搜索结果。

#### cURL 示例

```bash
curl -i \
--proxy brd.superproxy.io:33335 \
--proxy-user brd-customer-<CUSTOMER_ID>-zone-<ZONE_NAME>:<ZONE_PASSWORD> \
-k \
https://duckduckgo.com/?q=budget+laptops+under+500+gbp&kl=uk-en&kad=en-gb&df=w
```

#### Python 示例

```python
import requests
import urllib3

urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

host = "brd.superproxy.io"
port = 33335
username = "brd-customer-<CUSTOMER_ID>-zone-<ZONE_NAME>"
password = "<ZONE_PASSWORD>"
proxy_url = f"http://{username}:{password}@{host}:{port}"

proxies = {
http: proxy_url,
https: proxy_url
}

url = "https://duckduckgo.com/?q=budget+laptops+under+500+gbp&kl=uk-en&kad=en-gb&df=w"
response = requests.get(url, proxies=proxies, verify=False)

with open("duckduckgo-scraper-api-result.html", "w", encoding="utf-8") as file:
file.write(response.text)

print("Response saved!")
```

> 注意：在生产环境中使用原生代理方式时，建议安装 Bright Data 的 SSL 证书。请参考我们的[SSL 证书指南](https://docs.brightdata.com/general/account/ssl-certificate)。

👉 想查看完整 HTML 输出预览，请参见[完整结果](https://github.com/triposat/DuckDuckGo-Search-Scraper/blob/main/duckduckgo-scraper-api-output/duckduckgo-scraper-api-result.html)。

## DuckDuckGo 搜索查询参数

通过多种查询参数精准调优你的搜索结果。

### 本地化

#### 国家与语言（`kl`）

指定搜索结果的国家与语言。

示例：

```bash
curl --proxy brd.superproxy.io:33335 \
--proxy-user brd-customer-<id>-zone-<zone>:<password> \
https://duckduckgo.com/?q=best+coffee+brands&kl=it-it
```

返回意大利地区的定制化结果。

#### 界面语言（`kad`）

控制 DuckDuckGo 的界面语言。

示例：

```bash
https://duckduckgo.com/?q=photo+editing+tools&kad=de
```

搜索内容保持英文，但界面以德语显示。

### 安全搜索设置（`kp`）

调整成人内容过滤。

#### 取值

- `1` – 严格
- `-1` – 中等
- `-2` – 关闭

示例：

```bash
https://duckduckgo.com/?q=swimsuit&kp=1
```

仅返回“家庭安全”的结果。

### 时间范围筛选（`df`）

限定搜索结果的时间范围。

#### 取值

- `d` – 最近一天
- `w` – 最近一周
- `m` – 最近一月
- `y` – 最近一年
- 自定义范围：如 `2025-03-01..2025-03-10`

示例：

```bash
https://duckduckgo.com/?q=iphone+15+review&df=w
```

仅显示最近一周的评测。

### 设备定向（`brd_mobile`）

模拟来自不同设备类型的搜索。

#### 选项

- `0` – 桌面端（默认）
- `1` – 随机移动设备
- `ios` 或 `iphone` – iPhone
- `ipad` 或 `ios_tablet` – iPad
- `android` – 安卓手机
- `android_tablet` – 安卓平板

示例：

```bash
https://duckduckgo.com/?q=top+travel+apps&brd_mobile=ios
```

模拟 iPhone 用户，你可能会看到应用商店链接、移动端内容或 AMP 页面。

### 浏览器仿真（`brd_browser`）

为请求指定浏览器的 User-Agent。

#### 选项

- 默认（随机浏览器）
- `chrome` – Google Chrome
- `safari` – Safari
- `firefox` – Mozilla Firefox（不兼容 `brd_mobile=1`）

示例：

```bash
https://duckduckgo.com/?q=best+vpn+services&brd_browser=safari
```
模拟 Safari 浏览器，以便了解该平台上的展示与排名差异。

## 实用示例

你希望在英国市场，面向移动端用户，监测竞争对手“500 英镑以下的预算笔记本”相关页面的定价。

目标：

- 模拟英国移动端用户
- 获取本地化英文结果（英国零售商，英镑货币）
- 使用移动端 Chrome UA（捕获 AMP 等移动特化结果）
- 聚焦近期清单类文章或优惠

将需求组合成一个 cURL 命令：

```bash
curl --proxy brd.superproxy.io:33335 \
--proxy-user brd-customer-<CUSTOMER_ID>-zone-<ZONE_NAME>:<ZONE_PASSWORD> \
"https://duckduckgo.com/?\
q=budget+laptops+under+500+gbp&\
kl=uk-en&\
kad=en-gb&\
df=w&\
brd_mobile=android&\
brd_browser=chrome"
```
🎯 这将获取“移动优先、已本地化、且为近期”的内容。

## 支持与资源

- 文档：[SERP API 文档](https://docs.brightdata.com/scraping-automation/serp-api/)
- 相关 API：
- [SERP API](https://github.com/bright-cn/serp-api)
- [Google Search API](https://github.com/bright-cn/google-search-api)
- [Google News Scraper](https://github.com/bright-cn/Google-News-Scraper)
- [Google Trends API](https://github.com/bright-cn/google-trends-api)
- [Google Reviews API](https://github.com/bright-cn/google-reviews-api)
- [Google Hotels API](https://github.com/bright-cn/google-hotels-api)
- [Google Flights API](https://github.com/bright-cn/google-flights-api)
- [Web Unlocker API](https://github.com/bright-cn/web-unlocker-api)
- 使用场景：
- [SEO 与 SERP 追踪](https://www.bright.cn/use-cases/serp-tracking)
- [旅游行业数据](https://www.bright.cn/use-cases/travel)
- 拓展阅读：[最佳 SERP API](https://www.bright.cn/blog/web-data/best-serp-apis)
- 联系支持：[support@brightdata.com](mailto:support@brightdata.com)
