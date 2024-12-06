---
sidebar_position: 1
title: useCsRqAdvancedQueryLoadEvent
---

`useCsRqAdvancedQueryLoadEvent` は、API 呼び出し方式が Orval（拡張版）に対応する参照系 API ロードイベントを初期化するためのフックです。

## シグネチャ

<h3>
  <code>useCsRqAdvancedQueryLoadEvent<br/>&nbsp;&lt;TApiResponse><br/>(queryResult: RqAdvancedQueryResult<br/>&nbsp;&lt;TApiResponse>):<br/>CsRqAdvancedQueryLoadEvent<br/>&nbsp;&lt;TApiResponse></code>
</h3>

## 引数

| 引数名     | 必須 | 型                                                       | 説明                                                               |
| ---------- | ---- | -------------------------------------------------------- | ------------------------------------------------------------------ |
| queryResult| 〇   | `RqAdvancedQueryResult<TApiResponse>*¹`                  | TanStack Query の `useQuery` を使ったカスタムフックを指定します。   |

\*1：`RqAdvancedQueryResult`は API のレスポンスに関する情報を保持する型定義です。

## 返り値

API のレスポンス、成功・失敗のステータスなどの情報が含まれる`CsRqAdvancedQueryLoadEvent`クラスのインスタンスを返します。

## 使用例

```tsx
export const useTodoSearchView = (): TodoSearchView => {
  const keyword = useCsInputTextItem("検索キーワード", useInit(""), stringRule(true));

  return useCsView(
    {
      keyword: keyword,
      loadEvent: useCsRqAdvancedQueryLoadEvent(useSearchTodo({ keyword: keyword.value ?? "" } )),
    }
  );
};