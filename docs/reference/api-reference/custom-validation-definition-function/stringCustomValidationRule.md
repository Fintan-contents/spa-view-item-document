---
sidebar_position: 1
title: stringCustomValidationRule
---

`stringCustomValidationRule` は、指定されたバリデート関数とメッセージ関数を使用して、`string`型の入力項目に対するカスタムバリデーションルールを生成します。

バリデート関数とは、バリデーション処理の際に呼び出されるコールバック関数で、エラーとしたいときに `false` を返すよう実装します。コールバックの引数は、検証する値の `newValue` と検証対象の `item` が渡されます。

メッセージ関数とは、バリデーション処理がエラーとなった際に呼び出されるコールバック関数で、メッセージを文字列として返すよう実装します。コールバックの引数は、項目の `label`、検証した値の `value`、検証対象の `item` が渡されます。

## シグネチャ

<h3>`stringCustomValidationRule(validator, message): CustomValidationRule<string>`</h3>

## 引数

| 引数名    | 必須 | 型                                | 説明                                                                                                                                                                                                                                  |
| --------- | ---- | --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| validator | 〇   | `CustomValidator<string>*¹`       | バリデート関数を指定します。正規表現を用いてバリデーションを実施したい場合は、[createRegExpValidator](../../api-reference/custom-validation-helper-function/createRegExpValidator.md)というヘルパ関数で簡潔に実装することができます。 |
| message   | 〇   | `CustomValidateMessage<string>*²` | メッセージ関数またはメッセージを指定します。                                                                                                                                                                                          |

\*1：`CustomValidator`は バリデート関数で、以下の定義になります。

```ts
type CustomValidator<T> = (newValue: T | undefined, item: CsItem<T>) => boolean;
```

\*2：`CustomValidateMessage`はメッセージ関数で、以下の定義になります。

```ts
type CustomValidateMessage<T> =
  | ((label: string, value: T, item: CsItem<T>) => string)
  | string;
```

## 返り値

バリデート関数とメッセージ関数を保持した`CustomValidationRule<string>` クラスのインスタンスを返します。

## 使用例

```tsx
const myCustomValidationRules: CustomValidationRules = {
  nameRule: stringCustomValidationRule(
    createRegExpValidator(/^[A-Za-z ]*$/), // バリデート関数
    (label) => `${label}は、アルファベットと空白のみ使用可能です。` // メッセージ関数
  ),
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
    }
  ),
};
```
