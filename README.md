# agent-personal-skills

コーディングエージェント向けの**自作**個人スキル置き場。Cursor / Claude Code / Copilot など、使うツールを問わず全プロジェクトで共有する指示をここに集める。

上流（Anthropic / コミュニティ）の skill はここには置かない。`npx skills` で入れる。

ローカルのフォルダ名が違っていても、リモートリポジトリ名は `agent-personal-skills` を想定する。

## つなぎ方（正は `~/.agents`）

自作 skill の実体はこのリポ。ホームでは共通入口に symlink し、必要なら各エージェント用ディレクトリにもつなぐ。

```bash
# 共通（推奨）
mkdir -p ~/.agents/skills
ln -sfn "$PWD/check-skills-updates" ~/.agents/skills/check-skills-updates

# 使うツールだけ追加（例）
mkdir -p ~/.cursor/skills ~/.claude/skills
ln -sfn "$PWD/check-skills-updates" ~/.cursor/skills/check-skills-updates
ln -sfn "$PWD/check-skills-updates" ~/.claude/skills/check-skills-updates
```

今後自作を足したら同様に symlink する。

## このリポに入れるもの / 入れないもの

| 入れる | 入れない |
|--------|----------|
| 自作 `SKILL.md`（更新確認、git/gh 運用、自分用ワークフロー） | `frontend-design` など上流 skill のコピー |
| 上流 skill の install 手順（下のメモ） | `~/.agents/` の lock や生成物 |

プロジェクト固有の skill（例: 特定リポの業務ワークフロー）は、そのリポ配下（`.agents/skills/` や `.cursor/skills/` など）に置く。

## 上流 skill（デザイン周り・参考）

マシン初期セットアップや移行時:

```bash
npx skills add anthropics/skills --skill frontend-design -g -a cursor -a claude-code -y
npx skills add ibelick/ui-skills --skill baseline-ui -g -a cursor -a claude-code -y
```

（使うエージェントに合わせて `-a` を増減する。全部なら `--agent '*'`。）

更新確認は自作 skill `check-skills-updates`、または:

```bash
npx skills check
npx skills update -g -y
```

`npx skills` の実体は `~/.agents/skills/`。各ツール用ディレクトリへは CLI か手動 symlink で配る。

## 自作 skill 一覧

| name | 用途 |
|------|------|
| `check-skills-updates` | `npx skills` 管理のグローバル skill の更新確認・適用 |

## 今後寄せたい候補

- git / `gh` の個人運用（commit・PR・ブランチの自分ルールを skill 化）
- 繰り返し使っているプロンプトやチェックリスト

エージェント固有の短いルール（User Rules 等）と役割が被る場合は、長い手順・再現コマンドがあるものだけ skill にする。
