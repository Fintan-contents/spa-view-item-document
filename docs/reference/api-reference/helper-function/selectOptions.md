---
sidebar_position: 1
title: selectOptions
---

`selectOptions` は、セレクトボックスやマルチチェックボックスなどの選択肢に変換するための関数です。
類似のヘルパ関数に[selectOptionStrings](../helper-function/selectOptionStrings.md) と[selectOptionNumbers](../helper-function/selectOptionNumbers.md) があります。そちらも参照してください。

## シグネチャ

<h3>`selectOptions(options, optionValueKey?, optionLabelKey?): SelectOptions`</h3>

## 引数

| 引数名         | 必須 | 型       | 説明                                                                  |
| -------------- | ---- | -------- | --------------------------------------------------------------------- |
| options        | 〇   | `any[]`  | セレクトボックスの選択肢の配列を指定します。                          |
| optionValueKey |      | `string` | 各選択肢の値を示すキーを指定します。デフォルトは `"value"` です。     |
| optionLabelKey |      | `string` | 各選択肢のラベルを示すキーを指定します。デフォルトは `"label"` です。 |

## 返り値

選択肢の配列とキー情報を保持した `SelectOptions` クラスのインスタンスを返します。

## 使用例

```tsx
const countries = [
  { value: "jp", label: "日本" },
  { value: "us", label: "アメリカ" },
  { value: "uk", label: "イギリス" },
];

const users = [
  { id: "jp", name: "Alice", isAdmin: true },
  { id: "jp", name: "Bob", isAdmin: false },
  { id: "jp", name: "Charlie", isAdmin: false },
];

useCsView({
  country: useCsSelectBoxItem(
    "国",
    useInit(),
    stringRule(true),
    selectOptions(countries), // 第2、第3引数はデフォルトではvalueとlabelのため省略
    RW.Editable,
    "国を選択してください"
  ),
  assignee: useCsSelectBoxItem(
    "担当者",
    useInit(),
    stringRule(true),
    selectOptions(users, "id", "name"), // 第2、第3引数でidとnameを指定
    RW.Editable,
    "担当者を選択してください"
  ),
});
```
