---
sidebar_position: 2
title: Item間やEventとItemの間に依存関係があるとき
---

View で定義した Item 間で値を参照する場合や `XxxMutateButton` のイベントでリクエストに View で定義した Item の値を渡すような Event と Item の間に依存関係があるときには注意する点があります。

一例として、Event で Item の値を参照するような場合、同じブロックで Item, Event の初期化を行うと Event に Item の値を渡すことが出来なくなります。

Item を変数として定義することで Event 側で同じ View に定義されている Item の値を参照することができます。

```tsx title="Itemを外側に定義する"
export const useTodoSearchView = (): TodoSearchView => {
  // highlight-start
  // returnの外側に変数として定義する。
  const assignee = useCsInputTextItem(
    "担当者",
    useInit(""),
    stringRule(true, 1, 20),
    RW.Editable,
    "検索する担当者を入力してください",
  );
  // highlight-end
  return useCsView({
    assignee: assignee,
    searchTodo: useCsRqAdvancedQueryButtonClickEvent(
      useListTodo(
        // highlight-start
        { assignee_eq: assignee.value ?? "" },
        // highlight-end
        {
          query: {
            enabled: false,
            refetchOnWindowFocus: false,
          },
        },
      ),
    ),
  });
};
```
