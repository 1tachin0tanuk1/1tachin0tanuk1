# 🧭 開発ポリシー・命名規約・共通指針

## 👋 はじめに
このページは、私が開発を行う際の **基本方針・命名ルール・構造指針** をまとめたものです。  
将来的にチーム開発や組織（Org）へ移行した際にも一貫した開発運用を行えるよう、  
「再現性」「保守性」「引継ぎ性」を重視しています。

---

## 🏷️ リポジトリ命名規約
すべてのリポジトリ名は、以下の形式で統一します：

| プレフィックス | 意味 | 例 |
|----------------|------|------|
| `app-` | アプリケーション本体（Web・バッチ・CLIなど） | `app-order-ocr`, `app-kiln-monitor` |
| `lib-` | 共通ライブラリ・SDK | `lib-common`, `lib-sharepoint` |
| `infra-` | 環境構築・CI/CD・運用スクリプト | `infra-ci`, `infra-deploy` |
| `docs-` | ドキュメント・仕様・報告書など | `docs-energy-report`, `docs-ai-overview` |

> 🔹 命名は **小文字＋ハイフン（-）区切り**。  
> 🔹 環境名（dev / stg / prod）はリポジトリ名に含めず、ブランチやEnvironmentsで管理。

---

## 🧱 ディレクトリ構成（標準）

src/<package>/
core/ # ビジネスロジック（主要処理）
adapters/ # 外部接続層（API・DB・SharePoint等）
utils/ # 汎用関数・共通機能
tests/ # pytest等のテストコード
docs/ # セットアップ手順・設計資料

> 📘 **src構成**を採用し、Pythonのモジュールパス衝突を防止。  
> 📘 `docs/` には最低限の環境構築手順・設計意図を記述する。  

---

## ⚙️ コーディング・バージョン管理ルール

| 項目 | 内容 |
|------|------|
| コーディング規約 | Python: PEP8 / PEP257 準拠 |
| 型チェック | `mypy` / `pyright` 等で型安全性を担保 |
| Lint | `ruff` / `flake8` などをCIで自動実行 |
| テスト | `pytest` / `unittest` / `vitest` 等（自動化推奨） |
| コミットメッセージ | [Conventional Commits](https://www.conventionalcommits.org/ja/v1.0.0/) 準拠 |
| 例 | `feat: 新しいOCRモジュールを追加`, `fix: バグ修正`, `docs: READMEを更新` |
| ブランチ命名 | `main`, `feat/<機能>`, `fix/<修正>` |
| バージョンタグ | `v1.0.0`（Semantic Versioning） |

---

## 🔐 セキュリティと環境変数の扱い

| ファイル | 目的 | 注意点 |
|-----------|------|--------|
| `.env.example` | 環境変数の雛形 | リポジトリに含める（値は空でOK） |
| `.env` | 実際の値 | 絶対にGitに含めない |
| `.gitignore` | 除外リスト | `.env`, `__pycache__/`, `logs/` 等を登録 |
| Secrets | 機密値はGitHub SecretsまたはAzure Key Vaultで管理 |

---

## 🧩 ドキュメント運用
- 各プロジェクトに `README.md` を必ず配置  
- `README` の内容（最低限）  
  - 概要  
  - セットアップ手順  
  - 実行方法  
  - ディレクトリ構成  
  - 更新履歴（CHANGELOG）



実行などは別途整備していく・・・
