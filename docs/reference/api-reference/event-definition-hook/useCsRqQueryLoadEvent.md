---
sidebar_position: 1
title: useCsRqQueryLoadEvent
---

`useCsRqQueryLoadEvent` は、API 呼び出し方式が TanStack Query および Orval（シンプル版）に対応する参照系 API ロードイベントを初期化するためのフックです。

## シグネチャ

<h3>
  <code>useCsRqQueryLoadEvent<br/>&nbsp;&lt;TApiResponse><br/>(queryResult: UseQueryResult<br/>&nbsp;&lt;TApiResponse>):<br/>CsRqQueryLoadEvent<br/>&nbsp;&lt;TApiResponse></code>
</h3>

## 引数

| 引数名     | 必須 | 型                                                       | 説明                                                               |
| ---------- | ---- | -------------------------------------------------------- | ------------------------------------------------------------------ |
| queryResult| 〇   | `UseQueryResult<TApiResponse>*¹`                  | TanStack Query の `useQuery` を使ったカスタムフックを指定します。   |

\*1：`UseQueryResult`は API のレスポンスに関する情報を保持するTanStack Queryの組み込みの型定義です。

## 返り値

API のレスポンス、成功・失敗のステータスなどの情報が含まれる`CsRqQueryLoadEvent`クラスのインスタンスを返します。

## 使用例

```tsx
export const useTodoSearchView = (): TodoSearchView => {
  const keyword = useCsInputTextItem("検索キーワード", useInit(""), stringRule(true));

  return useCsView(
    {
      keyword: keyword,
      loadEvent: useCsRqQueryLoadEvent(useSearchTodo({ keyword: keyword.value ?? "" } )),
    }
  );
};