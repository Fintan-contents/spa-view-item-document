---
sidebar_position: 1
title: numberRule
---

`numberRule` は、数値入力項目のバリデーションルールを生成するための関数です。この関数では、必須項目かどうか、最小・最大値、カスタムルール名を指定できます。

## シグネチャ

<h3>`numberRule(required: boolean, min?: number, max?: number, customRuleName?: string): NumberValidationRule`</h3>

## 引数

| 引数名         | 必須 | 型        | 説明                                             |
| -------------- | ---- | --------- | ------------------------------------------------ |
| required       | 〇   | `boolean` | 入力項目が必須項目かどうかを指定します。         |
| min            |      | `number`  | 入力数値の最小値を指定します。                   |
| max            |      | `number`  | 入力数値の最大値を指定します。                   |
| customRuleName |      | `string`  | カスタムバリデーションルールの名前を指定します。 |

## 返り値

`number`型のバリデーション定義情報（必須項目かどうか、最小・最大文字数、カスタムルール名など）を保持する `NumberValidationRule` クラスのインスタンスを返します。

## 使用例

```tsx
const view = useCsView(
  {
    terminalNum: useCsInputNumberItem(
      "利用端末数",
      useInit(),
      numberRule(true, 1, 10, "正の整数")
    ),
  },
  {
    customValidationRules: myCustomValidationRules, // 「正の整数」のバリデーションルールを定義済み
  }
);
```
