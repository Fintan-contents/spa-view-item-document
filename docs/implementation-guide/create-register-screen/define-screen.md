---
sidebar_position: 2
title: 1. 画面を定義する
---

省力化コンポーネントでは、1 つの画面とその画面内に含まれる入力項目を View と Item という概念で定義します。

## View の型を定義する

View とは、複数の入力項目を含む 1 つの画面に対応する概念です。  
画面内の情報を View に集約することで、バリデーションスキーマの自動生成や入力項目の自動配置、画面単位で設定する項目の一元管理などが可能となります。

View の型を定義する際は、画面に配置する入力項目数分、項目の変数名と Item クラスの型のセットを記述します。その際は、 `CsView` という型を拡張する必要があります。

```tsx
type XxxView = CsView & {
  項目の変数名: Itemクラスの型;
  ...
}
```

Item とは、 1 つの入力項目に対応する概念です。ラベルや React の状態変数、バリデーションルールなどの入力項目に関する情報を Item の中に集約します。

省力化コンポーネントでは、テキストボックスやラジオボタン、チェックボックスなどの様々な入力形態に対応する Item クラスを提供しています。使用可能な Item クラス一覧については、[リファレンス](../../category/リファレンス)を参照してください。

以下に示すコードでは、[本節のゴール](goal.md)で示した画面を作るための View の型を、 `RegisterUserView` という名前で定義しています。

```tsx title="Viewの型を定義する"
type RegisterUserView = CsView & {
  userName: CsInputTextItem;
  password: CsInputPasswordItem;
  gender: CsRadioBoxItem;
  birthDay: CsInputDateItem;
  terminalNum: CsInputNumberItem;
};
```

## View を初期化する

View を初期化するためには、 `useCsView` という省力化コンポーネントのフックを使用します。 `useCsView` の引数には、`useCsXxxItem` というフックを使って初期化した Item を渡します。（ `useCsXxxItem` の `Xxx` は Item の種類に応じて異なります。）

```tsx
useCsView({
  項目の変数名: useCsXxxItem(ラベル名, 初期値, バリデーションルール, 選択肢*¹),
  ...
})

※1 選択肢を持つ入力項目のみ指定します
```

以下に示すコードでは、[本節のゴール](goal.md)で示した画面を作るための View の初期化処理を、`useRegisterUserView` という名前のカスタムフックとして定義しています。

```tsx title="Viewを初期化するカスタムフックを作成する"
const useRegisterUserView = (): RegisterUserView => {
  return useCsView({
    userName: useCsInputTextItem(
      "ユーザー名",
      useInit(""),
      stringRule(true, 3, 30),
    ),
    password: useCsInputPasswordItem(
      "パスワード",
      useInit(""),
      stringRule(true, 8, 16),
    ),
    gender: useCsRadioBoxItem(
      "性別",
      useInit(""),
      stringRule(true),
      selectOptionStrings(["男性", "女性", "回答しない"]),
    ),
    birthDay: useCsInputDateItem(
      "生年月日",
      useInit("2000-01-01"),
      stringRule(true),
    ),
    terminalNum: useCsInputNumberItem(
      "利用端末数",
      useInit(),
      numberRule(false, 1, 10),
    ),
  });
};
```

:::info
View の初期化に使用する `useCsView` 、Item の初期化に使用する `useCsXxxItem` 、および `useCsXxxItem` の内部で使用するヘルパ関数( `useInit` や `selectOptionStrings` など)のシグネチャについては[リファレンス](../../category/リファレンス)を参照してください。
:::

:::info
バリデーションルールの詳細については、[バリデーションを定義する](./define-validation.md)で説明します。
:::
