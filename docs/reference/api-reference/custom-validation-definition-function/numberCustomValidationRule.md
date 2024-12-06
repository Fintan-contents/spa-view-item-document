---
sidebar_position: 1
title: numberCustomValidationRule
---

`numberCustomValidationRule` は、指定されたバリデート関数とメッセージ関数を使用して、`number`型の入力項目に対するカスタムバリデーションルールを生成します。

バリデート関数とは、バリデーション処理の際に呼び出されるコールバック関数で、エラーとしたいときに `false` を返すよう実装します。コールバックの引数は、検証する値の `newValue` と検証対象の `item` が渡されます。

メッセージ関数とは、バリデーション処理がエラーとなった際に呼び出されるコールバック関数で、メッセージを文字列として返すよう実装します。コールバックの引数は、項目の `label`、検証した値の `value`、検証対象の `item` が渡されます。

## シグネチャ

<h3>`numberCustomValidationRule(validator, message): CustomValidationRule<number>`</h3>

## 引数

| 引数名    | 必須 | 型                                | 説明                                         |
| --------- | ---- | --------------------------------- | -------------------------------------------- |
| validator | 〇   | `CustomValidator<number>*¹`       | バリデート関数を指定します。                 |
| message   | 〇   | `CustomValidateMessage<number>*²` | メッセージ関数またはメッセージを指定します。 |

\*1：`CustomValidator`は バリデート関数で、以下の定義になります。

```ts
type CustomValidator<T> = (newValue: T | undefined, item: CsItem<T>) => boolean;
```

\*`2：CustomValidateMessage` はメッセージ関数で、以下の定義になります。

```ts
type CustomValidateMessage<T> =
  | ((label: string, value: T, item: CsItem<T>) => string)
  | string;
```

## 返り値

バリデート関数とメッセージ関数を保持した `CustomValidationRule<number>` クラスのインスタンスを返します。

## 使用例

```tsx
const myCustomValidationRules: CustomValidationRules = {
  positiveNumberRule: numberCustomValidationRule(
    // バリデート関数
    (newValue, item) => newValue !== undefined && newValue > 0,
    // メッセージ関数
    (label, newValue, item) => `${label}は正の数でなければなりません。`
  ),
};
```
