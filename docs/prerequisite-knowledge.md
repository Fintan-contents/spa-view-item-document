---
sidebar_position: 2
title: "前提知識"
---

# 前提知識

省力化コンポーネントを用いてアプリケーションを開発するにあたって、以下のカテゴリの技術知識が必要となります。

| カテゴリ                    | 技術                                         |
| --------------------------- | -------------------------------------------- |
| プログラミング言語          | JavaScript, TypeScript                       |
| フロントエンド技術スタック  | React, Next.js                               |
| UI コンポーネントライブラリ | Ant Design, Material UI, React Bootstrap     |
| バリデーションライブラリ    | Yup, Zod                                     |
| API 関連知識                | TanStack Query, OpenAPI Specification, Orval |

### プログラミング言語

| 技術       | 説明                                                                                                                                                                                                     |
| ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| JavaScript | ウェブアプリ開発に用いられるスクリプト言語です。                                                                                                                                                         |
| TypeScript | JavaScript に静的型付けを追加したプログラミング言語です。JavaScript と上位互換性があり、静的型付けによりコード実行前にエラーを検出できます。その性質から、開発規模が大きくなるほどその効果を発揮します。 |

### フロントエンド技術スタック

| 技術    | 説明                                                                                                                               |
| ------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| React   | コンポーネントベースのアプローチで、ウェブアプリ開発に用いられる JavaScript ライブラリです。                                       |
| Next.js | React をベースにしたフレームワークです。サーバーサイドレンダリングや静的サイト生成を簡単に実現するための強力なツールを提供します。 |

### UI コンポーネントライブラリ

:::warning
以下に示す 3 つの UI コンポーネントライブラリ全ての知識を持っている必要はありません。
プロジェクトで使用する UI コンポーネントライブラリに対する知識があれば十分です。
:::

| 技術            | 説明                                                                      |
| --------------- | ------------------------------------------------------------------------- |
| Ant Design      | エンタープライズ向けの高品質な React コンポーネントライブラリです。       |
| Material UI     | Google の Material Design に基づいた React コンポーネントライブラリです。 |
| React Bootstrap | Bootstrap フレームワークに基づいた React コンポーネントライブラリです。   |

### バリデーションライブラリ

:::warning
以下に示す 2 つのバリデーションライブラリ両方の知識を持っている必要はありません。
プロジェクトで使用するバリデーションライブラリに対する知識があれば十分です。
:::

| 技術 | 説明                                                                                                            |
| ---- | --------------------------------------------------------------------------------------------------------------- |
| Yup  | JavaScript のオブジェクトスキーマバリデーションライブラリです。 柔軟で使いやすいという特徴を持ちます。          |
| Zod  | TypeScript のオブジェクトスキーマバリデーションライブラリです。型安全性が高く、軽量であるという特徴を持ちます。 |

### API 関連知識

:::warning
以下に示す API 関連知識の全てを持っている必要はありません。
プロジェクトで採用する API 仕様に対する知識があれば十分です。
:::

| 技術                  | 説明                                                                                    |
| --------------------- | --------------------------------------------------------------------------------------- |
| TanStack Query        | バックエンドの API を呼び出すために使用するライブラリです。                             |
| OpenAPI Specification | API の仕様を記述するための標準規格です。                                                |
| Orval                 | OpenAPI 仕様から TypeScript の型定義と API クライアントコードを自動生成するツールです。 |

## 参考サイト

前提知識として必要な技術要素を学習するための参考サイトを紹介します。

### JavaScript Primer (JavaScript)

JavaScript の学習は[JavaScript Primer](https://jsprimer.net/)を参考にしてください。

JavaScript Primer は、JavaScript の文法や機能を一から学べるサイトです。[第一部：基本文法](https://jsprimer.net/basic/)までの知識があれば、最低限の JavaScript の知識は身に付いています。目次を見てわからない箇所があれば学習してください。

### サバイバル TypeScript (TypeScript)

TypeScript の学習は[サバイバル TypeScript](https://typescriptbook.jp/)を参考にしてください。

サバイバル TypeScript は、TypeScript を最短ルートで実務利用できることを目指したサイトです。[読んで学ぶ TypeScript](https://typescriptbook.jp/reference)の知識があれば、最低限の TypeScript の知識は身に付いています。目次を見てわからない箇所があれば学習してください。

### React 公式サイト (React)

React の学習は[公式サイト](https://ja.react.dev/)を参考にしてください。

React を利用したことがない人は[クイックスタート](https://ja.react.dev/learn)から始めることをお勧めします。  
「React を学ぶ」の内容が理解できていれば、最低限の React の知識は身に付いています。分からない箇所があれば学習してください。

### Next.js 公式サイト (Next.js)

Next.js の学習は[公式サイト](https://nextjs.org/)を参考にしてください。

省力化コンポーネントを使用するアプリケーション基盤として Next.js を採用しています。

### Ant Design 公式サイト (Ant Design)

Ant Design の学習は[公式サイト](https://ant.design/components/overview/)を参考にしてください。

### Material UI 公式サイト (Material UI)

Material UI の学習は[公式サイト](https://mui.com/material-ui/)を参考にしてください。

### React Bootstrap 公式サイト (React Bootstrap)

React Bootstrap の学習は[公式サイト](https://react-bootstrap.github.io/#:~:text=React-Bootstrap%20replaces%20the%20Bootstrap)を参考にしてください。

### Yup 公式サイト (Yup)

Yup の学習は[公式サイト](https://yup-docs.vercel.app/)を参考にしてください。

### Zod 公式サイト (Zod)

Zod の学習は[公式サイト](https://zod.dev/)を参考にしてください。

### TanStack Query 公式サイト (TanStack Query)

TanStack Query の学習は[公式サイト](https://tanstack.com/query/latest)を参考にしてください。  
特に [useQuery](https://tanstack.com/query/latest/docs/framework/react/reference/useQuery#usequery)、[useMutation](https://tanstack.com/query/latest/docs/framework/react/reference/useMutation#usemutation) は頻繁に使用するため、目を通しておくことをお勧めします。

### OpenAPI 公式サイト (OpenAPI Specification)

OpenAPI Specification の学習は[公式サイト](https://www.openapis.org/what-is-openapi)を参考にしてください。

:::info
[Swagger Editor](https://editor.swagger.io/)を使用することで API のリクエスト、レスポンスなどの詳細を確認できます。
API 仕様の内容を[Swagger Editor](https://editor.swagger.io/)のエディターに貼るとプレビューにその内容が表示されます。

その他の Swagger 機能については[What Is Swagger?](https://swagger.io/docs/specification/about/)を参照してください。
:::

### Orval 公式サイト (Orval)

Orval の学習は[公式サイト](https://orval.dev/)を参考にしてください。
