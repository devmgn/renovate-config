# renovate-config

Renovate共通設定プリセット

## 使い方

各リポジトリの`renovate.json`に以下を設定:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>devmgn/renovate-config"]
}
```

## 設定内容

- **ベース**: `config:best-practices`
- **タイムゾーン**: Asia/Tokyo
- **スケジュール**: 夜間（22時〜5時）
- **platformAutomerge**: 有効（GitHub native automerge使用）
- **ラベル**: `dependencies`, `renovate`
- **Dependency Dashboard**: 有効
- **postUpdateOptions**: `pnpmDedupe`（更新後に `pnpm dedupe` を実行）
- **osvVulnerabilityAlerts**: 有効（OSV ベースの脆弱性アラート）
- **`@types/*`**: `group:definitelyTyped` でまとめて更新

### カスタムマネージャー

- `customManagers:biomeVersions`
- `customManagers:githubActionsVersions`

### ロックファイルメンテナンス

- 日曜夜間に自動実行・自動マージ

### パッケージルール

- patchアップデートをグループ化
