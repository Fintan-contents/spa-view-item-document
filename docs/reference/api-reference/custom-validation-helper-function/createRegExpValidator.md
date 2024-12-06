---
sidebar_position: 3
title: createRegExpValidator
---

`createRegExpValidator`は、バリデーション関数を返すヘルパ関数です。正規表現パターンに基づいて入力値を検証するバリデーション関数を返します。[カスタムバリデーション定義の関数](../../../category/カスタムバリデーション定義の関数)で使用できます。

## シグネチャ

<h3>`createRegExpValidator(pattern: RegExp): CustomValidator<string>`</h3>

## 引数

| 引数名  | 必須 | 型         | 説明                                                                                                                     |
| ------- | ---- | ---------- | ------------------------------------------------------------------------------------------------------------------------ |
| pattern | 〇   | `RegExp*¹` | 入力値を検証するための正規表現パターンを指定します。指定したパターンに一致しない場合にバリデーションエラーが発生します。 |

\*1：`RegExp`は正規表現のための JavaScript の組み込みクラスです。

## 返り値

このヘルパ関数は、正規表現 `pattern` に一致するかどうかを判定するバリデート関数を返します。

## 使用例

```tsx
const customValidationRules: CustomValidationRules = {
  半角英字: stringCustomValidationRule(
    // highlight-start
    createRegExpValidator(/^[a-zA-Z]*$/), // 半角数字のみを許容する正規表現を定義
    // highlight-end
    (label: string) => `${label}は半角英字で入力してください`
  ),
  全角文字: stringCustomValidationRule(
    // highlight-start
    createRegExpValidator(/^[^ -~｡-ﾟ]*$/), // 全角文字のみを許容する正規表現を定義
    // highlight-end
    (label: string) => `${label}は全角文字で入力してください`
  ),
};
```
