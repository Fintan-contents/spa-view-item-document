---
sidebar_position: 1
title: booleanRule
---

`booleanRule` は、真偽値入力項目のバリデーションルールを生成するための関数です。この関数では、必須項目かどうか、カスタムルール名を指定できます。

## シグネチャ

<h3>`booleanRule(required: boolean, customRuleName?: string): BooleanValidationRule`</h3>

## 引数

| 引数名         | 必須 | 型        | 説明                                             |
| -------------- | ---- | --------- | ------------------------------------------------ |
| required       | 〇   | `boolean` | 入力項目が必須項目かどうかを指定します。         |
| customRuleName |      | `string`  | カスタムバリデーションルールの名前を指定します。 |

## 返り値

`boolean` 型のバリデーション定義情報（必須項目かどうか、カスタムルール名など）を保持する `BooleanValidationRule` クラスのインスタンスを返します。

## 使用例

```tsx
const view = useCsView(
  {
    isConfirmed: useCsInputCheckboxItem(
      "確認済み",
      useInit(false),
      // highlight-start
      booleanRule(true, "確認済み")
      // highlight-end
    ),
  },
  {
    customValidationRules: myCustomValidationRules, // 「確認済み」のカスタムバリデーションルールを定義済み
  }
);
```
