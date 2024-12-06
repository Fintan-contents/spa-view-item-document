---
sidebar_position: 1
title: useRangeInit
---

`useRangeInit` は、数値または文字列の範囲入力項目の初期値を設定するためのフックです。

## シグネチャ

<h3>`useRangeInit<T extends number | string>(lower?, upper?): [T[] | undefined, Dispatch<React.SetStateAction<T[] | undefined>>]`</h3>

## 引数

| 引数名 | 必須 | 型               | 説明                           |
| ------ | ---- | ---------------- | ------------------------------ |
| lower  |      | `T`              | 範囲の下限値を設定します。     |
| upper  |      | `T`              | 範囲の上限値を設定します。     |

## 返り値

`useState<T[]>([lower, upper])`の戻り値を返します。

## 使用例

```tsx
useCsView({
  // highlight-start
  budgetRange: useCsInputNumberRangeItem(
    "予算範囲",
    useRangeInit<number>(0, 1000),
    numberRule(false, 0, 10000),
    RW.Editable,
    "最低予算価格を入力してください",
    "最高予算価格を入力してください"
  ),
  // highlight-end
});