---
sidebar_position: 1
title: useInit
---

`useInit` は、入力項目の初期値を設定するためのフックです。このフックは[入力項目定義のフック](../../../category/入力項目定義のフック)にある`useCsXxxItem`で使用されます。内部実装は以下のようになっており、型引数 `T` および `undefined` を状態として返します。

```ts
export function useInit<T>(value?: T) {
  const state = useState<T | undefined>(value);
  return state;
}
```

状態に`undefined` を含める理由は数値のクリアなどに対応するためです。

## シグネチャ

<h3>`useInit<T>(value?: T): StateResult<T>`</h3>

## 引数

| 引数名 | 必須 | 型  | 説明                           |
| ------ | ---- | --- | ------------------------------ |
| value  |      | `T` | 入力項目の初期値を設定します。 |

## 返り値

`useState<T | undefined>(value)`の戻り値を返します。

## 使用例

```ts
useCsView({
  inputTextItem: useCsInputTextItem(
    "名前",
    // highlight-start
    useInit("Sample"),
    // highlight-end
    stringRule(true, 1, 10),
    RW.Editable
  ),
});
```
