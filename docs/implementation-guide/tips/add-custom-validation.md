---
sidebar_position: 5
title: カスタムバリデーションの追加方法
---

正規表現を用いたチェックや、パスワードに大文字・小文字・記号を最低一つ含めるなどの固有のバリデーションルールを追加したい場合は本節が役立ちます。

## カスタムバリデーションルールの生成

`stringCustomValidationRule` 関数を使用することで、`string`型に対するカスタムバリデーションルールを生成することができます。
引数にはバリデート関数とメッセージ関数を指定します。

## 正規表現を用いたカスタムバリデーションルールの生成

バリデーションルールを正規表現を用いて簡潔に記述できる場合は、バリデート関数に `createRegExpValidator` 関数を使用することで実現できます。

```tsx title="アルファベットと空白のみを許容するバリデーションルール"
const myCustomValidationRules: CustomValidationRules = {
  // highlight-start
  nameRule: stringCustomValidationRule(
    createRegExpValidator(/^[A-Za-z ]*$/), // バリデート関数
    (label) => `${label}は、アルファベットと空白のみ使用可能です。`, // メッセージ関数
  ),
  // highlight-end
};
```

## 独自のバリデーションルールの生成

独自のバリデート関数を実装して適用することができます。

以下の例では、パスワードのルールとして、大文字・小文字・記号・数字が使われているかをチェックしています。

```tsx title="パスワードの複雑な作成ルールを定義したバリデーションルール"
const myCustomValidationRules: CustomValidationRules = {
  // highlight-start
  passwordRule: stringCustomValidationRule(
    // バリデート関数
    (newValue, item) => {
      if (!newValue) {
        return true;
      }
      let count = 0;
      if (/[A-Z]/.test(newValue)) {
        count++;
      }
      if (/[a-z]/.test(newValue)) {
        count++;
      }
      if (/[0-9]/.test(newValue)) {
        count++;
      }
      if (/[!-)+-/:-@[-`{-~]/.test(newValue)) {
        count++;
      }
      return count >= 4;
    },
    // メッセージ関数
    (label, newValue, item) => {
      let requireds = ["大文字", "小文字", "数字", "記号"];
      if (/[A-Z]/.test(newValue)) {
        requireds = requireds.filter((e) => "大文字" !== e);
      }
      if (/[a-z]/.test(newValue)) {
        requireds = requireds.filter((e) => "小文字" !== e);
      }
      if (/[0-9]/.test(newValue)) {
        requireds = requireds.filter((e) => "数字" !== e);
      }
      if (/[!-)+-/:-@[-`{-~]/.test(newValue)) {
        requireds = requireds.filter((e) => "記号" !== e);
      }
      return `${label}は、${requireds.join("、")}を含めてください`;
    },
  ),
  //highlight-end
};
```

## 項目間バリデーション

バリデート関数内である Item の値に応じて別の Item の値をバリデーションを実施するような項目間バリデーションの実装方法について紹介します。

Item から親の View を取得し対象の Item の値を取得することができます。親の View を取得した際、型としては`CsView`となっているためキャストする必要がある点に注意してください。

```tsx
export type RegisterUserView = {
  name: CsInputTextItem;
  age: CsInputTextItem;
  mailAddress: CsInputTextItem;
  gender: CsRadioBoxItem;
  budget: CsInputNumberItem;
  // 中略
};
// バリデート関数
(newValue, item) => {
  // item: 金額の入力項目を定義したItem
  const parentView = item.parentView as RegisterUserView; // itemが定義されているViewを取得しキャスト
  const ageItem = parentView.age; // 年齢を取得
  //------
  // 年齢に応じた金額の範囲でバリデーション
  // -----
};
```

## カスタムバリデーションルールの適用

`useCsView`関数の引数 `options` に `stringCustomValidationRule`関数で定義したカスタムバリデーションルールを指定することで適用することができます。

また、下の例では `buildInCustomValidationRules` という事前に組み込みのカスタムバリデーションルールを定義したオブジェクトも合わせて展開しています。

```tsx
useCsView(
  {
    //  definitionsを指定
  },
  {
    customValidationRules: {
      ...buildInCustomValidationRules, // ビルドインカスタムバリデーションルール
      ...myCustomValidationRules, // 定義したカスタムバリデーションルール
    },
  },
);
```
