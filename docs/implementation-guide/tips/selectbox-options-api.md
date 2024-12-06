---
sidebar_position: 3
title: セレクトボックスの選択肢を API で取得する方法
---

セレクトボックスのオプションの値に API で取得した値を採用するようなオプションが動的に変わる場合に本節が役立ちます。

## セレクトボックスのオプションを動的に変えるには

`CsSelectBoxItem` の `setOptions` メソッドを使用することで実現できます。

`setOptions`の第一引数には API で取得するような動的に変わるオブジェクトを指定します。
第二引数には、選択肢の値にセットするプロパティ名を指定し、第三引数には選択肢の表示ラベルに使用するプロパティ名を指定します。

```tsx title="実装例"
type Users = {
  id: string;
  name: string;
  age: string;
  gender: string;
  mailAddress: string;
};
const loadUserView = useLoadUsersView();
const users = loadUsersView.loadUsersEvent.response ?? []; // Users型の配列
// highlight-start
todoCreateView.assignee.setOptions(users, "id", "name");
// highlight-end
```
