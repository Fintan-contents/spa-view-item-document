---
sidebar_position: 7
title: 6. 登録ボタンを配置する
---

API イベントの定義が完了したら、画面コンポーネントを使用して API 呼び出し用のボタンを配置していきます。
また、`CsMutateButtonClickEvent` に関しては、リクエストデータを設定する処理を別途記述する必要があります。

## ボタンを配置する

登録ボタンを配置する際は、画面コンポーネントとして `AxMutateButton` を使用します。（型定義で用いた `CsMutateButtonClickEvent` に対応した画面コンポーネントを使用します。）

`event` という Props に、対応するイベントの変数を指定します。また、`validationViews` に View の変数を指定することで、バリデーションが実行できます。

```tsx title="登録ボタンを配置する"
// 対象画面の View を初期化する
const view = useRegisterUserView();
return (
  <>
    {/* 入力項目を配置する */}
    <AxTableLayout view={view} colSize={1} />
    {/* highlight-start */}
    {/* 登録ボタンを配置する */}
    <AxMutateButton
      type="primary"
      event={view.registerButton}
      validationViews={[view]}
    >
      登録する
    </AxMutateButton>
    {/* highlight-end */}
  </>
);
```

:::warning
`AxTableLayout` は Item で定義された入力項目のみ自動配置されるため、ボタンは手動で配置する必要があります。
:::

## API リクエストデータを設定する

更新系の API を呼び出す際は、リクエストデータを設定する必要があります。

リクエストデータを設定するためには、イベント変数が持つ `setRequest` というメソッドを使用します。各リクエストパラメータに、Item 変数の value を指定します。

```tsx title="イベント変数にリクエストデータを設定する"
const view = useRegisterUserView();

// highlight-start
// リクエストデータを設定する
view.registerButton.setRequest({
  data: {
    userName: view.userName.value ?? "",
    password: view.password.value ?? "",
    gender: view.gender.value ?? "",
    birthDay: view.birthDay.value ?? "",
    terminalNum: view.terminalNum.value,
  },
});
// highlight-end

return (
  <>
    {/* 入力項目を配置する */}
    <AxTableLayout view={view} colSize={1} />
    {/* 登録ボタンを配置する */}
    <AxMutateButton
      type="primary"
      event={view.registerButton}
      validationViews={[view]}
    >
      登録する
    </AxMutateButton>
  </>
);
```

:::info
`userName: view.userName.value ?? ""` は、`value` が `undefined` の時は代わりに空文字を指定する、という処理です。  
必須のリクエストパラメータに `undefined` を指定すると型エラーが発生するため、それを避けるために上記の処理を行なっています。
:::

## API 呼び出しを確認する

モックサーバを起動し、登録ボタンの押下によって API が呼び出されることを確認します。

OpenAPI からモックサーバを簡単に立ち上げられるツールとして、Mockoon や Prism があります。公式サイトを参照し、各自モックサーバの起動を行ってください。

- [Mockoon 公式サイト](https://mockoon.com/)
- [Prism 公式サイト](https://stoplight.io/open-source/prism/)

:::info
[省力化コンポーネントのサンプルアプリケーション](https://github.com/Fintan-contents/dev-react-cs-example/tree/develop)では Mockoon を使用しています。
:::

モックサーバの起動が完了したら、入力項目に任意の値を入力して登録ボタンを押下してください。

`AxMutateButton` の `successMessage` という Props に文字列を指定しておくことで、API 呼び出しが成功したかどうかを確認することができます。

```tsx
<AxMutateButton
  type="primary"
  event={view.registerButton}
  validationViews={[view]}
  successMessage="登録に成功しました"
>
  登録する
</AxMutateButton>
```

また、開発者ツールのネットワークタブからも API リクエストのステータスを確認することができます。

![API呼び出しのデモ](/img/api_call.gif)
