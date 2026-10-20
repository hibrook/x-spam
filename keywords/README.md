# x-spam keywords

X (Twitter) 黄推清道夫关键词库。把本目录内的文件放到仓库的 `keywords/` 下（注意不要再嵌套一层 `keywords/keywords/`）。

## 文件说明

| 文件 | 作用 | 脚本是否读取 |
|---|---|---|
| `absolute.txt` | 绝对屏蔽词，命中即屏蔽。只放高置信度词 | 是 |
| `highrisk.txt` | 高风险词，只加分，不单独触发屏蔽 | 是 |
| `patterns.txt` | JS 正则，一行一条，写单反斜杠（`\d`），不要写 `\\d` | 是 |
| `whitelist.txt` | 正常口语，用于降低误杀，不覆盖绝对词和强正则 | 是 |
| `trusted_accounts.txt` | 可信账号 `@handle`，命中后跳过所有规则 | 是 |
| `review_only.txt` | 人工审核区：泛词、疑似人名/站名、被停用的规则 | 否 |
| `version.json` | 版本信息 | 是 |

## 维护约定

- 新词先放 `highrisk.txt` 或 `review_only.txt`，确认高置信度后再升到 `absolute.txt`。
- 单个泛词（如 `AI`、`主页`、`免费`）不要放进 `highrisk.txt`，容易和“英文 Handle + 中文名”之类的结构叠加分数造成误杀；泛词的导流含义用 `patterns.txt` 里的组合规则表达。
- 比已有绝对词更长且包含它的词是冗余的，不需要再加。
- 正则里不要用无界的 `.*`，用 `.{0,N}`。
- 每次改动后更新 `version.json`。
