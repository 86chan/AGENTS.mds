# AGENTS.mds

AIコーディングエージェント向けの役割定義と設計書運用ガイドライン集。

## 概要

本リポジトリは、AIエージェントを各言語・プラットフォームのアーキテクトとして振る舞わせるための `AGENTS.md` を集めたものです。UNIX哲学と各言語の最新イディオムを軸に、コード生成・レビュー・ドキュメント作成の基準を定めます。

各ファイルはそのままプロジェクトのルートに `AGENTS.md` として配置し、エージェントの振る舞いを統一するために利用できます。

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

基本設計（specs）で「何をするか」を定め、詳細設計（core）で「どう実現するか」を言語非依存に定める。詳細設計は基本設計を前提として導出する。

## 共通する思想

すべての役割定義に共通するUNIX哲学ベースの原則。

1. **Do One Thing and Do It Well** — 単一責任、短い関数（理想20行以内）
2. **Small is Beautiful** — 継承よりコンポジション、KISS、過剰な抽象化を避ける
3. **Make Every Program a Filter** — データをパイプのように流す宣言的記述、純粋関数
4. **Silence is Golden** — エラーを握りつぶさない、型安全性・Null安全性の厳格適用

## 設計書運用の特徴

- **I/O分離**: コアエンジンは外部I/Oを持たず、操作や時間は外部から注入する
- **決定論**: 同じ入力に対し、どの言語でも同じ結果になる（標準乱数・OSタイマー禁止）
- **データとロジックの分離**: 変化しうる仕様はDSL（データ）として定義する
- **設計書と実装の分離**: TypeScriptからRustへ変えても書き直し不要な内容に限定する
- **ファイル命名**: `ARC-001_...md`、`INT-001_...md`、`DSL-001_...md`、`SCR-001_...md`、`BIZ-001_...md` 等

## 使い方

1. 利用する言語・プラットフォームに該当するファイルを選ぶ
2. プロジェクトのルートに `AGENTS.md` としてコピーまたはリネームする
3. 設計書を運用する場合は `docs/specs/Specs.md`、`docs/core/Core.md`、`docs/impl/Impl.md` を参照する

