---
sidebar_position: 1
title: numberArrayRule
---

`numberArrayRule` は、数値配列入力項目のバリデーションルールを生成するための関数です。この関数では、必須項目かどうか、カスタムルール名を指定できます。

## シグネチャ

<h3>`numberArrayRule(required: boolean, customRuleName?: string): NumberArrayValidationRule`</h3>

## 引数

| 引数名         | 必須 | 型        | 説明                                             |
| -------------- | ---- | --------- | ------------------------------------------------ |
| required       | 〇   | `boolean` | 入力項目が必須項目かどうかを指定します。         |
| customRuleName |      | `string`  | カスタムバリデーションルールの名前を指定します。 |

## 返り値

`number[]` 型のバリデーション定義情報（必須項目かどうか、カスタムルール名など）を保持する `NumberArrayValidationRule` クラスのインスタンスを返します。

## 使用例

```tsx
const view = useCsView(
  {
    scores: useCsInputNumberArrayItem(
      "スコア",
      useInit([]),
      // highlight-start
      numberArrayRule(true, "スコアのカスタムルール")
      // highlight-end
    ),
  },
  {
    customValidationRules: myCustomValidationRules, // 「スコア」のカスタムバリデーションルールを定義済み
  }
);
```
