# 課題提出

**AIと考えた1セッションのログ**
## Part 1：AIと考えた1セッション
テーマ: week10で学んだJSの機能について完成例と自分が実装した物を比較しながら教えてもらう

送った指示
**目的**: ユーザー情報表示ツールのコードの役割・機能を教えてほしい
**前提**: 一つのツールと完成している実装例と自分が実装した物をAIに投げかけている。
見てほしい観点: 完成例と自分の実装を比較して、不足している部分を理由(○○は○○の役割があるため、実装に必要。のような形式で解説してもらう)と共に教えてもらう。console.log(users) の役割と書く場所、userList.textContent = "" の役割、.className と .textContentの違い、card.appendChild(...) に card と書く理由、userList.appendChild(card)の役割。
**制約**: コードの役割とその必要性の解説はしてほしいが、勝手に自分の実装にどう当てはめたらいいかの案を提示しないでほしい。
**出力形式**: 理由、例示
完成例を投げかけているので、コードの役割の解説に加えてそれがその完成例にどう影響を与えているかの説明がほしい。

**返ってきた出力（要約）**

1. console.log(users) の役割と書く場所
APIから取得したデータの中身を確認するために書きます。

javascript
const users = await response.json(); // データを取得
console.log(users); // ← 取得直後に書くことで中身を確認できる

取得した直後に書くのが一般的です。開発中の確認用なので、完成したら削除してOKです。


2. userList.textContent = "" の役割
表示エリアを空にする役割があります。
ボタンを押すたびに再取得する場合、空にしないと前のデータと新しいデータが重複して表示されてしまいます。

userList なのは、document.getElementById("userList") で取得した要素を入れた変数名がそのまま使われているからです。

3. .className と .textContent
javascript
const name = document.createElement("h2");
name.className = "text-lg font-bold"; // タグにクラスを追加する
name.textContent = user.name; // タグの中にテキストを入れる


4. card.appendChild(...) に card と書く理由
name と email を card の中に入れるためです。

javascript
const card = document.createElement("div");  // 箱を作る
const name = document.createElement("h2");   // 名前を作る
const email = document.createElement("p");   // メールを作る

card.appendChild(name);  // cardの中にnameを入れる
card.appendChild(email); // cardの中にemailを入れる


5. userList.appendChild(card)
完成した card を画面の userList に追加する処理です。
userList（画面の表示エリア）
　└ card（1人分のカード）
　　　├ name（名前）
　　　└ email（メール）

card.appendChild で部品を組み立てて、最後に userList.appendChild で画面に出すイメージです。


**"なぜ"を聞いた記録**
- 聞いたこと: 最後にconsole.error(error)って書く理由は何？
- 返ってきた説明（要約）: エラーの詳細をコンソールに表示するため。前文のuserList.textContent = "データの取得に失敗しました。"; は、画面上にメッセージを表示するためである一方で、console.error(error); は、開発者向けに詳細なエラー内容を表示するという目的がある。
- 聞く前は分からなかったが、聞いて分かったこと: 聞く前は、userList.textContentだけでエラーが出ていることを表示できると思っていたため、console.error(error);の必要性が分かっていなかったが、聞いてみてそれはコンソールでエラーの詳細を表示するためなのだと分かった。

**出力の4分類**

| 分類 | 内容 | 判断理由 |
自分の実装が終わった後に、AIに完成例と要件に沿って実装してもらった。インプットの完成例にはなかったものの、week11の課題提出の要件には「テキスト入力欄でGitHubのユーザー名を受け取る」「ボタンを押すとAPIにリクエストを送る」とあったため、AIは検索する機能を実装した。今回の課題においては、検索機能については触れられていなかったため、その機能は採用しなかった。

| 採用する | | |　JSの書き方
| 保留する | | |　GitHubのAPIは認証なしだと1時間に60回までしかリクエストできないことの説明。
| 採用しない | | |　検索ボタン
| 要確認 | | |　JSで習っていない書き方

---

## Part 2：流された場面の振り返り

week10の非同期処理の手順とFetchとJSONの意味・役割
→ AIにコードに意味を解説してもらい、理解した気になっていたから。

---

## Part 3：今後のAI利用方針

### Week11で気づいたこと

AIに頼り過ぎていると、いつの間にか分かった気になって自分のものになっていないのだと気づかされた。AIを使ったあとには、必ず自力でやってみることが重要だと思った。

### 自分のAI利用ルール

AIを使うときは、目的・前提・見てほしい観点・制約・出力形式のすべてを明確に提示する。
AIを使ったあとにAIを閉じた状態で、自分の言葉で説明してみる。
AIに丸ごと実装してもらうのではなく、各コードにフォーカスして、その意味・役割を教えてもらうようにする。
