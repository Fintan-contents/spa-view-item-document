---
sidebar_position: 6
title: 5. APIイベントを定義する
---

省力化コンポーネントで API 通信を行う際は、イベントという概念を用います。イベントとは、特定のタイミングやユーザ操作（ボタンクリックなど）によって実行される処理の情報を集約したものです。

## API イベントについて

API に関するイベントは、自動実行が可能な **LoadEvent** と、ユーザ操作（ボタン押下）によって実行可能な **ButtonClickEvent** の 2 種類があります。

<h3> LoadEvent </h3>

画面表示時などに自動で実行できる API イベントです。初回ロード時に画面で表示したいデータを取得する、といった用途で使用できます。一般の GET を使った検索では`CsQueryLoadEvent`、POST を使ってリクエストボティを必要とするような複雑な検索では`CsMutateLoadEvent`を使用します。

LoadEvent で使用する型と初期化フックは次の表の通りです。（※対応する画面コンポーネントはありません。）

| リクエスト | 型                  | フック                        | 画面コンポーネント |
| ---------- | ------------------- | ----------------------------- | ------------------ |
| GET        | `CsQueryLoadEvent`  | `useCsXxxQueryLoadEvent` \*¹  | なし               |
| POST       | `CsMutateLoadEvent` | `useCsXxxMutateLoadEvent` \*¹ | なし               |

＊1：`Xxx` は API 呼び出し方式によって異なります。[API 呼び出し方式の選択](../../introduction-guide/introduction-tool.md#api-呼び出し方式の選択)で「Orval(シンプル版)」もしくは「TanStack Query」 を選択した場合は`Rq`、「Orval(拡張版)」 を選択した場合は `RqAdvanced` から始まる部品を使用します。

<h3>ButtonClickEvent</h3>

ボタン押下によって実行できる API イベントです。検索ボタンや送信ボタンを実装する際に使用できます。参照系 API を呼び出す場合は`CsQueryButtonClickEvent`、更新系 API を呼び出す場合は`CsMutateButtonClickEvent`を使用します。

以下に対応表を示します。

| リクエスト              | 型                         | フック                               | 画面コンポーネント  |
| ----------------------- | -------------------------- | ------------------------------------ | ------------------- |
| GET                     | `CsQueryButtonClickEvent`  | `useCsXxxQueryButtonClickEvent` \*¹  | `AxQueryButton` \*² |
| POST<br/>PUT<br/>DELETE | `CsMutateButtonClickEvent` | `useCsXxxMutateButtonClickEvent` \*¹ | `AxMutateButton`\*² |

＊1：`Xxx` は API 呼び出し方式によって異なります。[API 呼び出し方式の選択](../../introduction-guide/introduction-tool.md#api-呼び出し方式の選択)で「Orval(シンプル版)」もしくは「TanStack Query」 を選択した場合は`Rq`、「Orval(拡張版)」 を選択した場合は `RqAdvanced` から始まる部品を使用します。  
＊2：`Ax` は Ant Design に対応した画面コンポーネントです。

## イベントの型を定義する

ここからは、登録用の API を用いて、ボタン押下時に入力値をサーバーに送信する処理の実装手順について解説します。

:::warning

ハンズオン形式で進めたい方は、 [実装ガイドのハンズオンで使用する API クライアントコードの生成手順](../../introduction-guide/working-after-introduction/orval-setting.md#実装ガイドのハンズオンで使用する-api-クライアントコードの生成手順) に従って API クライアントコードを作成してください。

<h4>以降の解説で登場するAPIクライアント関数 / 型</h4>
| 名前                  |  説明                                                                 |
|-------------------------|-------------------------------------------------------------------------------|
| `usePostUser`   | 登録用APIを呼び出すためのクライアント関数   |
| `PostUserBody`          | 登録用APIのリクエストデータ型   | 
:::

まず初めに、イベントの型を定義します。  
イベントの型定義では、Item と同様、イベントの変数名とイベントクラスの型のセットを記述します。

```tsx
イベントの変数名: CsXxxEvent<リクエストデータ型, レスポンスデータ型, エラー型>;
```

:::note
型引数に指定する項目は、イベントの種類によって異なります。
| イベントクラス名 | リクエストデータ型 | レスポンスデータ型 | エラー型 |
|-----------------------------|--------------------|--------------------|----------|
| `CsQueryLoadEvent` | なし | 必須 | 任意 |
| `CsMutateLoadEvent` | なし | 必須 | 任意 |
| `CsQueryButtonClickEvent` | なし | 任意 | 任意 |
| `CsMutateButtonClickEvent` | 必須 | 任意 | 任意 |
:::

以下に示すコードでは、 [1. 画面を定義する](./define-screen.md#view-の型を定義する) で定義した View の型に、登録ボタン用のイベントの型定義を追加しています。

更新系の API をボタン押下時に呼び出す場合は、 `CsMutateButtonClickEvent` を使用します。型引数には、リクエストデータ型として `{data: PostUserBody}` を指定します。

```tsx title="Viewの型定義に登録ボタン用のイベントを追加する"
type RegisterUserView = CsView & {
  userName: CsInputTextItem;
  password: CsInputPasswordItem;
  gender: CsRadioBoxItem;
  birthDay: CsInputDateItem;
  terminalNum: CsInputNumberItem;
  // highlight-start
  registerButton: CsMutateButtonClickEvent<{
    data: PostUserBody;
  }>;
  // highlight-end
};
```

## イベントを初期化する

イベントを初期化するためには、`useCsXxxEvent` という省力化コンポーネントのフックを使用します。フックの引数には、API を呼び出すためのクライアント関数の実行結果を指定します。

```tsx
useCsView({
  ...
  イベントの変数名: useCsXxxEvent(useApiClient()), // APIを呼び出すためのクライアント関数（useApiClient()）を指定
})
```

<br/>
以下に示すコードでは、[1. 画面を定義する](./define-screen.md#view-の型を定義する) で定義した View にイベントの初期化処理を追加しています。

フックとして、型定義で用いた `CsMutateButtonClickEvent` に対応する、 `useCsRqMutateButtonClickEvent` を使用します。  
フックの引数には、登録用 API を呼び出すためのクライアント関数 `usePostUser` の実行結果を指定します。

:::warning
Orval（拡張版）を選択している場合は、フックとして `useCsRqAdvancedMutateButtonClickEvent` を使用してください。
:::

```tsx title="イベントの初期化処理を追加する"
const useRegisterUserView = (): RegisterUserView => {
  return useCsView(
    {
      userName: useCsInputTextItem(
        "ユーザー名",
        useInit(""),
        stringRule(true, 3, 30),
      ),
      //
      // (...他の画面項目定義は省略...)
      //
      // highlight-next-line
      registerButton: useCsRqMutateButtonClickEvent(usePostUser());
    },
  );
};
```

:::info
本節で解説していない `CsQueryLoadEvent` や `CsQueryButtonClickEvent` を用いた実装方法については、[CRUD 機能を作る](../../category/crud機能を作る) で解説しています。`CsMutateLoadEvent`については本ドキュメントでは解説していません。
:::
