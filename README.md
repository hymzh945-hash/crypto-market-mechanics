# 书站部署说明（Crypto Market Mechanics static site）

全部离线可打开，零依赖、零 JS 库、单文件自洽。

## 目录

```
05_站点/
├── index.html                     书的落地页（含 Book 结构化数据 + 4 个购买链接）
├── tools/
│   ├── unlock-calculator.html     代币解锁抛压计算器
│   └── fee-calculator.html        真实费率成本计算器
├── robots.txt
└── sitemap.xml
```

## 已验证

- 两个计算器页的内联 JS 通过 `node --check` 语法校验
- index.html 的 JSON-LD 解析正常（`@type: Book`，4 个 `Offer`）
- `div` / `p` 标签开闭数量一致（index 8/8、9/9；unlock 14/14；fee 15/15）
- 两个计算器打开即算，不需要点按钮：默认值 → 解锁 −16.7%、费率 0.100%/回合

## 上线（两条路，都免费）

### A. Cloudflare Pages（推荐，无需信用卡、无需买域名）
1. 打开 `dash.cloudflare.com` → Workers & Pages → Create → Pages → Upload assets
2. 项目名随意（如 `crypto-market-mechanics`）
3. 把这四个文件按原目录结构拖进去上传
4. 得到 `xxx.pages.dev` 的公开地址，先用它当正式域名

### B. GitHub Pages
1. 新建仓库（Public）
2. 上传这四个文件，保证 `index.html` 在根目录
3. Settings → Pages → Source: `Deploy from a branch` → `main` / `/ (root)`
4. 得到 `用户名.github.io/仓库名/`

## 上线后必做的两件（决定能不能被搜到）

1. **Google Search Console**（`search.google.com/search-console`）：添加资源 → 验证（DNS 或 HTML 标签）→ 提交 `sitemap.xml`
2. **Bing Webmaster / IndexNow**（`bing.com/webmasters`）：同样提交 sitemap，Bing 提交后会较快被抓

> 注意：现在文件里的 `https://cryptomarketmechanics.example/`、`https://example.com/` 是**占位域名**。真实域名确定后必须全站替换（`index.html` 的 canonical、`sitemap.xml`、`robots.txt` 三处），否则 Search Console 会拒绝 sitemap。

## 后续可加的 SEO 页面（按优先级）

1. 28 章每章一页（先做被搜索最多的三章：解锁抛压、做市商贷款、费率分层）
2. 3–4 个计算器（还差：清算价、上市抛压推演）
3. 一个 `/glossary` 术语页（`maker fee`、`taker fee`、`cliff unlock`、`FDV`），术语页最容易吃到长尾
```
