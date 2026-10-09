# 团队技能仓库

本仓库托管团队内部使用的 Trae 技能（Skills），存放于 `.trae/skills/` 目录下。

## 技能与维护人

| 技能 | 路径 | 主 Owner | 备 Owner |
|------|------|----------|----------|
| boss-reply | `.trae/skills/boss-reply/` | @RiceShowerererer | @MiYuyuyuyu |
| weekly-report | `.trae/skills/weekly-report/` | @RiceShowerererer | @MiYuyuyuyu |

> 每个技能均设置主、备两名 Code Owner。提 PR 时，如果作者本人是 Code Owner，GitHub 不会将作者自动加入评审人，因此至少需要另一名 Owner 评审通过才能合并。

## 目录结构

```
.
├── .trae/
│   └── skills/
│       ├── boss-reply/       # Boss 回复技能
│       └── weekly-report/    # 周报生成技能
├── .github/
│   └── CODEOWNERS            # 代码所有者配置
├── .gitignore
├── .env.example              # 环境变量示例（复制为 .env 后填值）
└── README.md
```

## Clone 仓库

```bash
git clone <仓库地址> ~/team-repo
cd ~/team-repo
```

## 本地开发

1. 复制环境变量模板并填入真实值：

```bash
cp .env.example .env
# 编辑 .env，填入 FEISHU_APP_ID / FEISHU_APP_SECRET / DATA_API_TOKEN
```

2. `.env` 已被 `.gitignore` 忽略，不会提交到仓库。

## 提交合并请求（Pull Request）

1. 从 `main` 拉取最新代码，创建功能分支：

```bash
git checkout main
git pull
git checkout -b feature/your-change
```

2. 技能类改动提交前先跑评测（改了 `.trae/skills/` 下文件时必须执行）：

```bash
cd .trae/skills/<技能名>
python3 scripts/run_evals.py
```

全绿（全部用例通过）才继续提交流程；不绿先修，不要直接提交。

3. 提交修改并推送：

```bash
git add <相关文件>
git commit -m "描述你的改动"
git push -u origin feature/your-change
```

4. 在 GitHub 上发起 Pull Request，目标分支为 `main`。

5. 等待 Code Owner 评审。根据 `.github/CODEOWNERS` 配置，修改 `boss-reply` 或 `weekly-report` 目录下文件的 PR 需要至少一名 Owner 评审通过。

6. 评审通过后合并：合并方式选 **Create a merge commit**，不要选 Squash and merge（保留完整提交历史，方便追溯每次技能改动）。

7. 合并后回终端打 tag（网页面板里没有打 tag 的按钮）：

```bash
git checkout main
git pull
git tag <tag名>          # 例如 weekly-report-v1.1
git push origin <tag名>
```
