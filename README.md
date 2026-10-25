# AGENTS.mds

AIコーディングエージェント向けの役割定義と設計書運用ガイドライン集。

## 概要

本リポジトリは、AIエージェントを各言語・プラットフォームのアーキテクトとして振る舞わせるための `AGENTS.md` と、設計書運用ガイドラインを集めたものです。UNIX哲学と各言語の最新イディオムを軸に、コード生成・レビュー・ドキュメント作成の基準を定めます。

## リポジトリ構成

### 役割定義（言語・プラットフォーム別）

| ファイル | 対象 |
| :--- | :--- |
| `AGENTS.md` | 汎用テンプレート（プレースホルダ付き） |
| `Rust.md` | Rust（Rust 2024/2021、所有権、`tracing`、`cargo clippy`） |
| `Kotlin.md` | Android / Kotlin（Jetpack Compose、Coroutines、Clean Architecture/MVVM） |
| `Swift-ObjC.md` | Appleプラットフォーム（Swift 6 Concurrency、POP、Objective-C相互運用） |
| `Typescript.md` | TypeScript（Strictモード、`any` 禁止、Vitest/Jest） |
| `dotnet.md` | .NET / C#（.NET 10、record、Span<T>、Nullable参照型） |
| `Python.md` | Python（型ヒント、frozen dataclass、pytest、mypy --strict） |

### 設計書運用ガイドライン

| ファイル | 位置づけ | 対象 |
| :--- | :--- | :--- |
| `docs/specs/Specs.md` | 基本設計 | 画面仕様・業務仕様の運用（SCR / BIZ / COM 分類） |
| `docs/core/Core.md` | 詳細設計（言語非依存） | I/O分離、決定論、DSL、スキーマ分離 |
| `docs/impl/Impl.md` | 実装設計（言語固有） | モジュール構成、クラス割り当て、フレームワーク選定 |

ファイル命名: `ARC-xxx` / `INT-xxx` / `DSL-xxx` / `COM-xxx` / `SCR-xxx` / `BIZ-xxx` / `IMP-{lang}/IMP-xxx` / `DEF-000`

基本設計（specs）で「何をするか」を定め、詳細設計（core）で「どう実現するか」を言語非依存に定める。詳細設計は基本設計を前提として導出する。

## 共通する思想

すべての役割定義に共通するUNIX哲学ベースの原則。

1. **Do One Thing and Do It Well** — 単一責任、短い関数（理想20行以内）
2. **Small is Beautiful** — 継承よりコンポジション、KISS、過剰な抽象化を避ける
3. **Make Every Program a Filter** — データをパイプのように流す宣言的記述、純粋関数
4. **Silence is Golden** — エラーを握りつぶさない、型安全性・Null安全性の厳格適用

## 設計書運用の特徴

3層構成（基本設計 → 詳細設計 → 実装設計）と共通ルールは `docs/COMMON.md` と `docs/README.md` を参照。

## 使い方

1. 利用する言語・プラットフォームに該当するファイルを選ぶ
2. プロジェクトのルートに `AGENTS.md` としてコピーまたはリネームする
3. 設計書を運用する場合は `docs/COMMON.md`、`docs/specs/Specs.md`、`docs/core/Core.md`、`docs/impl/Impl.md` を参照する
