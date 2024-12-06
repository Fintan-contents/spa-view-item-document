---
sidebar_position: 3
title: Orvalの設定
---

:::warning

API 呼び出し方式の選択で「TanStack Query」を選択した方はこの作業を実施する必要がありません。
:::

Orval を用いて OpenAPI 仕様からコードを自動生成するための設定手順について解説します。  
設定手順は以下の 4 ステップです。

1. OpenAPI の定義ファイルを配置する
2. orval.config.ts を作成する
3. Axios のカスタムインスタンスを作成する
4. コードを自動生成する

## 1. OpenAPI の定義ファイルを配置する

OpenAPI 仕様が定義された `openapi.yml` を配置します。

```
プロジェクトのルート
　　|- openapi
　　　　|- openapi.yml　※配置場所はあくまで一例です
　　|- ...
```

:::info
省力化コンポーネントのサンプルアプリでは[openapi_todo.yaml](https://github.com/Fintan-contents/dev-react-cs-example/blob/develop/openapi/openapi_todo.yaml)を使用しています。  
:::

## 2. orval.config.ts を作成する

`orval.config.ts` という Orval の設定ファイルをプロジェクトのルート直下に作成します。

```
プロジェクトのルート
　　|- orval.config.ts
　　|- ...
```

設定ファイルに記述する内容は[Configuration(公式サイト)](https://orval.dev/reference/configuration/overview)を参照してください。  
最低限設定する必要がある項目は `input` と `output` です。

- [input](https://orval.dev/reference/configuration/input)：参照元の OpenAPI 仕様
- [output](https://orval.dev/reference/configuration/output)：自動生成されるコードに関する設定  
  ※ `mutator` には、手順 3 で作成するカスタムインスタンスを設定してください。

:::info
省力化コンポーネントのサンプルアプリでは[orval.config.ts](https://github.com/Fintan-contents/dev-react-cs-example/blob/develop/orval.config.ts)を使用しています。
:::

## 3. Axios のカスタムインスタンスを作成する

Orval に設定するための Axios のカスタムインスタンスを作成します。
カスタムインスタンスを作成することで、API リクエストに必要な共通設定を一元化できます。

```
プロジェクトのルート
　　|- src
　　　　|- libs
　　　　　　|- backend
　　　　　　　　|- customInstance.ts　※配置場所はあくまで一例です
```

省力化コンポーネントは、Axios のカスタムインスタンスを以下の表に示す<u>シンプル版</u>と<u>拡張版</u>の 2 種類に定義しています。

| 種類       | 説明                                                                                                                                                                                                                                                                                                                                       |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| シンプル版 | <ul><li>最低限必要な設定が記述されたシンプルな構成</li><li>API リクエストの返り値の型は、`Promise<any>` （TanStack Query を用いた場合と同様）</li></ul>※作成方法は、[Orval の公式サイト](https://orval.dev/guides/custom-axios#custom-instance)を参照してください                                                                          |
| 拡張版     | <ul><li>シンプル版の設定に加え、キャンセル時やタイムアウト時のエラーハンドリングが記述された拡張版</li><li>API リクエストの返り値の型は、`Promise<AxiosResponse<any, any>>`</li></ul>※作成方法は、[省力化コンポーネントのサンプルアプリケーション](https://github.com/Fintan-contents/dev-react-cs-example/tree/develop)を参照してください |

## 4. コードを自動生成する

1 ～ 3 の設定を行うことで、Orval を利用したコードの自動生成が行えるようになります。  
まず、 `package.json` に以下の定義を追記してください。

```js title="package.json"
{
  ...
  "scripts": {
    ...
    "code-gen": "npx orval --config ./orval.config.ts"
  },
  ...
}
```

次に、ターミナルで以下のコマンドを実行してください。実行後、手順 3 で `output` の中に指定した出力先にソースコードが自動生成されます。

```bash title="Terminal"
npm run code-gen
```

:::note

### 実装ガイドのハンズオンで使用する API クライアントコードの生成手順

[実装ガイド > 登録画面を作る](../../category/登録画面を作る) では、ハンズオン形式で API 呼び出し処理の実装方法について解説しています。  
その中で使用する API クライアントコードの作成手順を以下に示します。

<h4>1. OpenAPI の定義ファイルを配置する</h4>
ハンズオンでは、以下のOpenAPI仕様書を用いています。

<details>
  <summary>ハンズオンで使用するOpenAPI</summary>

```yml title="openapi.yml"
openapi: 3.0.0
info:
  title: User API
  version: "1.0.0"
  description: User registration API for submitting user information
paths:
  /user:
    post:
      summary: Register a new user
      description: Creates a new user with specified information.
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                userName:
                  type: string
                  description: User's username
                password:
                  type: string
                  description: User's password
                gender:
                  type: string
                  description: User's gender
                birthDay:
                  type: string
                  description: User's birth date
                terminalNum:
                  type: number
                  description: Optional terminal number for the user
              required:
                - userName
                - password
                - gender
                - birthDay
      responses:
        "201":
          description: User created successfully
        "400":
          description: Invalid input
```

</details>

<h4>2. orval.config.ts を作成する</h4>
[省力化コンポーネントのサンプルアプリで使用している設定ファイル](https://github.com/Fintan-contents/dev-react-cs-example/tree/develop)と同様の内容で作成します。  
※ `target` には、1で作成したymlファイルを指定します。

```yaml
input: {
  // highlight-next-line
  target: "./openapi/openapi.yaml",
},
```

<h4>3. Axios のカスタムインスタンスを作成する</h4>
[Orval の公式サイト](https://orval.dev/guides/custom-axios#custom-instance)と同様の内容で、シンプル版のカスタムインスタンスを作成します。

<h4>4. コードを自動生成する</h4>
[手順4](#4-コードを自動生成する)を実行し、以下のような構成でAPIクライアントコードが自動生成されます。  
※ 生成場所は、`orval.config.ts` の設定内容によって変わります。
```terminal
//root//
　　└── src
　　　　├── framework
　　　　└── libs 
// highlight-start
　　　　　　└── generated
　　　　　　　　├── default - APIクライアントコード
　　　　　　　　└── model - 型定義
// highlight-end
```
:::

<hr/>
以上で、Orval の設定は完了です。  
自動生成されたコードを用いて実際に API を呼び出す方法については、[CRUD 機能の実装](../../implementation-guide/crud/goal.md)を参照してください。
