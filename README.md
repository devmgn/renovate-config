# renovate-config

Renovate 共通設定プリセット

## 使い方

各リポジトリの `renovate.json`:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>devmgn/renovate-config"]
}
```

## ポリシー

- **ベース**: `config:best-practices`（推奨設定・Dependency Dashboard・`group:recommended`・各種 helpers をまとめて有効化）
- **タイムゾーン**: Asia/Tokyo (`:timezone(Asia/Tokyo)`)
- **スケジュール**: 平日業務時間外 + 週末 (`schedule:nonOfficeHours`)
- **automerge スケジュール**: 同上 (`schedule:automergeNonOfficeHours`)
- **automerge 方式**: GitHub native automerge (`platformAutomerge`)
- **ラベル**: `dependencies`, `renovate`
- **脆弱性アラート**: OSV ベース (`osvVulnerabilityAlerts`)

## 自動マージ

| 対象 | 動作 | 仕掛け |
|---|---|---|
| `@types/*` の patch / minor | PR を作って自動マージ | `:automergeTypes` |
| lockfile maintenance | 週次（月曜未明）、PR を作らずブランチで直接マージ | `:maintainLockFilesWeekly` + `automergeType: branch` |

それ以外（通常の patch / minor / major）は手動レビュー。

## グルーピング

- `@types/*` を 1 PR にまとめる (`group:definitelyTyped`)
- React / linters / monorepo / test 系などエコシステム別のグルーピングは `config:best-practices` 経由の `group:recommended` で有効

## GitHub Actions

- バージョン文字列の同期: `customManagers:githubActionsVersions`
- SHA digest pin: `helpers:pinGitHubActionDigests`（`config:best-practices` 経由で有効）
- digest 更新を SemVer 認識させる: `helpers:pinGitHubActionDigestsToSemver`

## パッケージマネージャー

- pnpm: 更新後に `pnpm dedupe` を実行 (`postUpdateOptions: ["pnpmDedupe"]`)。npm / yarn 利用時は no-op
