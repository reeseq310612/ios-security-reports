# 补丁生效核验：从 build 号到 CVE 映射的设备端确认方法

**文章定位**：iOS 补丁治理 / 漏洞修复验证 / 企业资产管理
**研究范围**：Coruna 与 DarkSword 相关漏洞的修复版本、设备端标识、MDM 盘点口径与验收方法
**说明**：本文讨论核验流程与判断边界，不提供任何利用代码；版本与 CVE 信息以 Apple 安全公告和公开披露为准，不同来源存在差异时保留差异。

## 摘要

在 Coruna 与 DarkSword 的讨论中，最常见的一句安慰是“已经升到最新系统了”。这句话在个人设备上通常够用，在企业环境里却远远不够。原因有三个：同一 marketing 版本可能存在不同 build；一条攻击链的多个漏洞往往在不同版本分批修复；旧设备收到的回补版本与主线版本并不对应。

因此，“补丁是否生效”不是一个是或否的问题，而是一条证据链：设备版本号 → build 号 → CVE 修复矩阵 → 实际配置与缓解措施。本文给出一套可以在半天内落地的核验方法，并说明哪些结论可以下、哪些只能标注为“无法判定”。

## 第一章 为什么“最新”不等于“修完”

### 1.1 一条链的补丁是分批到达的

以公开披露的 DarkSword 为例，六个漏洞的修复分布在多个版本：

| 漏洞 | 层面 | 公开修复版本 |
| --- | --- | --- |
| CVE-2025-31277 | JavaScriptCore | iOS 18.6 |
| CVE-2025-43529 | JavaScriptCore | 18.7.3 / 26.2 |
| CVE-2026-20700 | 用户态 PAC 绕过 | iOS 26.3 |
| CVE-2025-14174 | GPU / ANGLE | 18.7.3 / 26.2 |
| CVE-2025-43510 | 内核 | 18.7.2 / 26.1 |
| CVE-2025-43520 | 内核提权 | 18.7.2 / 26.1 |

一台停在 iOS 18.7.2 的设备，可能已经修好了两个内核问题，却仍然暴露于 18.7.3 才修复的 JSC 与 ANGLE 漏洞。此时设备设置里显示“已是最新”，在它的版本分支上可能确实如此，但相对完整链条仍缺两环。

### 1.2 旧设备走的是另一条版本线

Coruna 的公开影响区间是 iOS 13.0–17.2.1。苹果在 2026 年 3 月为部分旧系统回补了补丁。回补版本通常只修特定问题，版本号也停留在旧主线上。拿它和“最新 iOS”比较没有意义，必须回到“该 build 是否包含对应 CVE 的修复”。

### 1.3 build 号才是设备端的最小事实

版本号是营销标识，build 号才是构建标识。同一版本在不同机型、不同批次上可能对应不同 build；Beta、候选版与正式版也可能共享相似版本号。企业做合规判断时，应同时采集版本号与 build 号，并以 Apple 安全公告中的产品与版本描述为准。

## 第二章 三个标识：版本、build 与 CVE

### 2.1 版本号解决“大致区间”

版本号适合做第一层筛选：低于某个版本直接判定为暴露；高于某个版本进入下一层核验。它不适合单独作为“已修复”的证据。

### 2.2 build 号解决“具体构建”

build 号通常由数字与字母组成，机型与版本之间可能不同。核验时应记录完整字符串，不要只记录前缀。对于 MDM 纳管设备，可以直接查询系统属性；对于未纳管设备，只能通过“设置 → 通用 → 关于本机”人工读取或让用户截图。

### 2.3 CVE 映射解决“到底修了什么”

Apple 的 Security Releases 页面按产品列出每个版本修复的 CVE。核验时建议建立一张自己的映射表，只保留与组织风险相关的条目，而不是照抄全部公告。表至少包含四列：CVE、受影响组件、修复版本、证据链接。

以 Coruna 相关公开编号为例，CVE-2024-23222 在 iOS 17.3 修复；CVE-2021-30952、CVE-2023-41974、CVE-2023-43000 等曾被 CISA KEV 收录。它们并不是“23 个新零日”，而是被重新组合的旧问题。对防守方而言，这意味着**旧设备上的旧 CVE 仍然具有现实价值**。

## 第三章 设备端核验流程

### 3.1 第一步：采集

需要采集的最小字段如下：

| 字段 | 来源 | 用途 |
| --- | --- | --- |
| 设备型号 | 关于本机 / MDM | 判断系统分支与升级上限 |
| iOS 版本 | 关于本机 / MDM | 第一层筛选 |
| build 号 | 关于本机 / MDM | 精确构建判断 |
| 是否纳管 | MDM | 决定能否远程核查 |
| 最后上线时间 | MDM | 判断数据是否新鲜 |
| 是否开启锁定模式 | 设备 / MDM 部分可见 | 缓解措施核验 |
| 自动更新状态 | 设备 / MDM | 解释滞后原因 |

### 3.2 第二步：对照

把设备分为三类：

- **已修复**：版本与 build 均落在公告列出的修复构建范围内，且相关 CVE 全部覆盖。
- **部分修复**：修好了链条中的一部分，但仍缺至少一个环节。这类设备应视为“可利用性下降，但未消除”。
- **无法判定**：版本信息缺失、build 不匹配、设备长期离线、或处于厂商未明确说明的 Beta 分支。

第三类最容易被忽略。很多企业报表把“无法判定”直接算成“合规”，这是自欺欺人。

### 3.3 第三步：验证缓解措施

补丁之外，还要核验缓解措施是否真的开启：

- 锁定模式是否启用（高价值目标）；
- 是否允许锁定状态下连接 USB 配件；
- 是否安装了不必要的配置描述文件；
- 是否使用企业代理或证书固定，导致网络侧检测失效；
- 是否开启被盗设备保护与高级数据保护。

这些配置不能替代补丁，但会改变攻击链的实际成功率与后果。

### 3.4 第四步：形成结论

建议的输出不是“合规/不合规”二分，而是一张分级表：

| 等级 | 判定 | 处置 |
| --- | --- | --- |
| A | 全部相关 CVE 已修复，缓解措施到位 | 常规监控 |
| B | 全部相关 CVE 已修复，缓解措施不足 | 30 天内补齐配置 |
| C | 部分修复 | 7 天内升级或隔离 |
| D | 无法判定 | 人工核查，暂按高风险处理 |
| E | 已确认暴露且无法升级 | 替换设备或进入例外审批 |

## 第四章 组织级实现

### 4.1 MDM 查询

多数 MDM 可以查询 `os_version`、`build_version`、`model`、`last_checkin` 等属性。把查询结果落到资产表，按“版本 + build”聚合，比逐台看设备高效得多。

一个可用的伪查询如下：

```sql
SELECT model, os_version, build_version, COUNT(*) AS devices
FROM mobile_assets
WHERE platform = 'iOS'
  AND last_checkin > NOW() - INTERVAL '7 days'
GROUP BY model, os_version, build_version
ORDER BY devices DESC;
```

### 4.2 阈值与例外

阈值应写成制度，而不是某位管理员的记忆：

- 所有纳入管理的 iPhone 不得低于组织规定的最低版本；
- 低于阈值的设备必须在 7 天内升级，否则进入例外审批；
- 无法升级的旧设备单独建账，限制其访问敏感系统的权限；
- Beta 设备不纳入生产合规基线，单独标记。

### 4.3 自动告警

把“新版本发布”和“新 CVE 修复”做成两条告警：前者提醒升级，后者提醒核验。只盯版本发布，会漏掉旧分支的回补；只盯 CVE，会缺少升级节奏。

## 第五章 常见误差

1. **只看版本号，不看 build**。同一版本不同构建可能包含不同修复。
2. **把“检查更新无结果”当成已修复**。设备可能停留在不再收主line更新的旧分支。
3. **把“未发现利用”当成“已修复”**。没有发现不等于没有暴露。
4. **忽略旧设备回补**。回补版本号低，但可能已修复关键 CVE，不能简单按版本高低判断。
5. **把 Beta 当成更安全**。Beta 的版本号可能更高，但不适合作为生产合规依据。
6. **报表把“未知”算成“合规”**。未知应单列，并按高风险处理。

## 第六章 验收清单

- [ ] 资产表同时包含版本号与 build 号；
- [ ] 已建立 Coruna/DarkSword 相关 CVE 的修复映射表；
- [ ] 每台设备有“已修复/部分修复/无法判定”的结论；
- [ ] 旧设备与 Beta 设备单独建账；
- [ ] 锁定模式、USB 配件、描述文件等缓解措施已核验；
- [ ] 低于阈值的设备有升级或例外审批记录；
- [ ] 告警同时覆盖“新版本”与“新 CVE”；
- [ ] 每季度复核一次映射表与资产表。

## 结语

补丁核验的价值，不在于生成一张漂亮的合规报表，而在于回答一个具体问题：**这台设备距离攻击链失效，还差哪一环？** 对 Coruna 与 DarkSword 这类多漏洞链条，答案往往不是“最新”或“不最新”，而是“修好了几环、还剩几环、剩下的那环有没有缓解措施”。

把这个问题问清楚，比争论“23 个漏洞还是 6 个漏洞”更有意义。

---

**咨询iOS系统安全相关问题，请联系 Telegram：https://t.me/one00190**

## 资料来源

- [Apple Security Releases](https://support.apple.com/en-us/100100)
- [Apple Platform Security Guide](https://support.apple.com/guide/security/welcome/web)
- [Google Threat Intelligence Group：Coruna: The Mysterious Journey of a Powerful iOS Exploit Kit](https://cloud.google.com/blog/topics/threat-intelligence/coruna-powerful-ios-exploit-kit)
- [Google Threat Intelligence Group：The Proliferation of DarkSword](https://cloud.google.com/blog/topics/threat-intelligence/darksword-ios-exploit-chain)
- [CISA Known Exploited Vulnerabilities Catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog)
- [NIST SP 800-40 Rev. 4：Guide to Enterprise Patch Management Planning](https://csrc.nist.gov/pubs/sp/800/40/r4/final)
- [Malwarebytes：Apple patches Coruna exploit kit flaws for older iOS versions](https://www.malwarebytes.com/blog/news/2026/03/apple-patches-coruna-exploit-kit-flaws-for-older-ios-versions)
