---
sidebar_position: 1
title: モチベーション
---

# モチベーション

## 従来の React 開発の冗長さ

React は、Web 画面開発において UI を宣言的に記述できる強力なライブラリです。

React を使用することで複雑なインタラクティブ UI の構築が容易になり、コンポーネントベースの設計によって再利用性や保守性が向上します。

その一方で、従来の React 開発では、状態変数やイベントハンドラ、バリデーションスキーマなどが重複して記述される傾向があり、コードの冗長さが目立ちます。  
以下に挙げる 4 つのポイントは、 React 開発で見られる典型的なコードの冗長さを示しています。

<strong>
- 分散して記述される入力項目の定義
- 類似したイベントハンドラの重複
- 画面全体のバリデーションスキーマの定義
- 画面項目コンポーネントの外部に記述される処理や定義
</strong>

### 分散して記述される入力項目の定義

1 つの入力項目に対して、状態変数、イベントハンドラ、バリデーション、コンポーネントなどをそれぞれ個別に定義する必要があります。

また、それに伴って項目を表す変数名やラベル名を何度も書くことになります。

```tsx
export const ConventionalPane: React.FC = () => {

  // 1つの入力項目(ユーザー名)に関連する定義が分散している

  // 状態変数
  const [userName, setUserName] = useState("")
 
  // (...省略...)

  // イベントハンドラ
  const onChangeUserName = (e: React.ChangeEvent<HTMLInputElement>) => {
    setUserName(e.target.value)
  }
 
  // (...省略...)

  // バリデーション
  const validationSchema = {
    userName: stringField().required(getRequiredMessage("ユーザー名"))
      .minLength(3, getMinLengthMessage("ユーザー名", 3))
      .maxLength(30, getMaxLengthMessage("ユーザー名", 30)),
 
  // (...省略...)

  // コンポーネント
  <div>
    <Typography.Text>ユーザー名</Typography.Text>
  </div>
  <Input
    value={userName}
    onChange={onChangeUserName}
  />
  <ValidationError message={error.userName} />
```

### 類似したイベントハンドラの重複

入力項目が複数ある場合、変数名や関数名が異なるだけでほとんど同じ内容のイベントハンドラを項目数分記述する必要があります。

```typescript
// 項目数分の類似したイベントハンドラ
const onChangeUserName = (e: React.ChangeEvent<HTMLInputElement>) => {
  setUserName(e.target.value);
};
const onChangePassword = (e: React.ChangeEvent<HTMLInputElement>) => {
  setPassword(e.target.value);
};
const onChangeMailAddress = (e: React.ChangeEvent<HTMLInputElement>) => {
  setMailAddress(e.target.value);
};
const onChangeGender = (e: RadioChangeEvent) => {
  setGender(e.target.value);
};
```

### 画面全体のバリデーションスキーマの定義

バリデーションを実施する場合、画面ごとにバリデーションスキーマの定義を記述する必要があります。

記述方法は使用するバリデーションライブラリによって異なりますが、項目ごとに記述する内容は似通っており(異なるのは項目名やバリデーションルールの設定値のみ)、コードが冗長になってしまいます。

以下に、Yup というバリデーションライブラリを使用してスキーマ定義を記述するコード例を示します。

```typescript
// メッセージ関数
const getRequiredMessage = (fieldName) => `${fieldName}は必須です`;
const getMinLengthMessage = (fieldName, minLength) =>
  `${fieldName}は最低${minLength}文字必要です`;
const getMaxLengthMessage = (fieldName, maxLength) =>
  `${fieldName}は最大${maxLength}文字までです`;

// バリデーションスキーマ
const validationSchema = yup.object().shape({
  userName: yup
    .string()
    .required(getRequiredMessage("ユーザー名"))
    .min(3, getMinLengthMessage("ユーザー名", 3))
    .max(30, getMaxLengthMessage("ユーザー名", 30)),
  password: yup
    .string()
    .required(getRequiredMessage("パスワード"))
    .min(8, getMinLengthMessage("パスワード", 8))
    .max(16, getMaxLengthMessage("パスワード", 16)),
  mailAddress: yup
    .string()
    .email("メールアドレスが無効です")
    .required(getRequiredMessage("メールアドレス")),
  gender: yup.string().required(getRequiredMessage("性別")),
  birthDay: yup.string().required(getRequiredMessage("誕生日")),
});
```

:::warning
上記に示したバリデーションスキーマは画面ごとに定義する必要があるため、例えば画面が 50 個ある場合、実装者は上記の定義を 50 画面分記述することになります。
:::

### 画面項目コンポーネントの外部に記述される処理や定義

React 開発においては、入力部品やボタンといった画面項目に関連する処理や定義がコンポーネントの外部に分散して記述されます。これにより、コードが冗長になり、保守性や可読性が低下する問題が生じます。
以下に、具体的な例を示します。

#### <strong>入力部品の場合</strong>

一般的な入力項目には、ラベルやバリデーションメッセージの表示領域が必要になります。

しかし、これらを毎回実装者が個別に記述するのは手間がかかり、コードの冗長さを引き起こします。さらに、項目ごとにラベル位置やメッセージ位置を適切に配置し、画面内でスタイルが統一されるように実装者が意識する必要もあります。

```tsx
// ユーザー名フォーム
<div className={styles.formStyle}>
  {/* ラベル */}
  <div className={styles.labelStyle}>
    <Typography.Text>ユーザー名</Typography.Text>
  </div>
  {/* 入力部品 */}
  <div className={styles.inputStyle}>
    <Input value="{userName}" onChange="{onChangeUserName}" />
  </div>
  {/* バリデーションメッセージ領域 */}
  <div className={validationStyle}>
    <ValidationError message="{error.userName}" />
  </div>
</div>
```

#### <strong>ボタンの場合</strong>

API 呼び出しやバリデーション実行など、ボタンを押下したときに実行したい処理は、コールバック関数として定義した上でボタンコンポーネントに渡す必要があります。

また、ローディング中のスピナー表示やボタン押下後のメッセージ表示などもコンポーネントの外部に記述する必要があります。これらの処理を毎回実装者が個別に記述するのは手間がかかり、コードの冗長さを引き起こします。

```tsx
// 送信ボタンを実装するために必要なコード

// ローディング判定用の状態変数
const [loading, setLoading] = useState(false);
// ボタン押下後に表示するメッセージを格納する状態変数
const [message, setMessage] = useState("");

// ボタン押下時に実行されるコールバック関数
const handleClick = async () => {
  // ローディング開始
  setLoading(true);
  setMessage("");

  // バリデーション実行処理
  executeValidation();

  try {
    // API呼び出し処理
    const response = callApi();
    const result = await response.json();

    // 成功メッセージの表示
    setMessage(`成功: ${result.message}`);
  } catch (error) {
    // 失敗メッセージの表示
    setMessage(`エラー: ${error.message}`);
  } finally {
    // ローディング終了
    setLoading(false);
  }
};

// コンポーネント
// (...省略...)

// 送信ボタン
<div className="buttonStyle">
  {/* 送信後のメッセージを表示する領域 */}
  {message && <div className="messageStyle">{message}</div>}
  {/* ボタン */}
  <Button onClick={handleClick} disabled={loading}>
    {/* ローディング中はスピナーを表示 */}
    {loading ? <Spinner /> : "送信"}
  </Button>
</div>;
```

<hr/>
次節で紹介する<strong>省力化コンポーネントのコンセプト</strong>は、上記に挙げた React 開発における冗長さを解消するためのアプローチです。
