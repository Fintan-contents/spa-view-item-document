---
sidebar_position: 1
title: 事前準備
---

# 事前準備

:::warning
[導入指標](../know-cs-component/introduction-index.md)をまだ読んでいない方は、まずそちらをご覧ください。
導入指標と自身のシステムを比較検討し、省力化コンポーネントの導入を決めた場合にのみ、以下の内容をお読みください。
:::

本章では、省力化コンポーネントをプロジェクトに導入するための手順について説明します。

まず初めに、事前準備として必要となる以下の 3 つの作業について説明します。

- Node.js のインストール
- Next.js プロジェクトの作成
- 導入ツールのダウンロード

## Node.js のインストール

:::warning
既に Node.js がインストールされている方は、[Next.js プロジェクトの作成](#nextjs-プロジェクトの作成)に進んでください。
:::

[Node.js の公式サイト](https://nodejs.org/en)より、LTS 版をインストールしてください。

## Next.js プロジェクトの作成

:::warning
既に Next.js プロジェクトを作成済みの方は、[導入ツールのダウンロード](#導入ツールのダウンロード)に進んでください。
:::

以下に示すリンク先 (Next.js 公式サイト) を参照し、Next.js プロジェクトの作成を行ってください。

:::warning
プロジェクトを作成するときは、以下の 2 点に注意してください。

- バージョンは <u><strong>14 系</strong></u>を選択してください。（次節で登場する省力化コンポーネントの導入ツールは、バージョン 14 系の Next.js プロジェクトに対応しています。）
- ルーティング方式は <u><strong>App Router</strong></u> を選択してください。（Pages Router は現在非推奨となっています。）
  :::

- [Next.js プロジェクトの作成](https://nextjs.org/docs/getting-started/installation#automatic-installation)
- [アプリの起動](https://nextjs.org/docs/getting-started/installation#run-the-development-server)

## 導入ツールのダウンロード

省力化コンポーネントの資材をインストールするためのツールが、GitHub の [dev-react-cs-component](https://github.com/Fintan-contents/dev-react-cs-component) リポジトリに格納されています。

Git をインストールしている場合は、以下のコマンドでリポジトリをクローンしてください。

```bash title="Terminal"
$ git clone https://github.com/Fintan-contents/dev-react-cs-component.git
```

Git をインストールしていない、もしくは使わない場合は、以下のリンクから zip ファイルをダウンロードし、任意の場所に解凍してください。

[GitHub から zip ファイルをダウンロード](https://github.com/Fintan-contents/dev-react-cs-component/archive/refs/heads/main.zip)
