# チャージ＆アタック（横長オンライン対戦版）

ChromebookとスマホのChromeで使う、横向き1画面の対戦ゲームです。まだ公開していません。ルームコードはデモではなく実際の通信から表示します。

## ルール
- チャージ：+1、相手のハーを受けると負け
- ハー：チャージ1以上、1消費。相手のチャージに勝つ
- バリア：必要チャージ0、ハーを防ぐ
- ミラー：チャージ3以上、3消費。ハーを反射する
- 2人が選択してから開示・判定。決着なしなら次へ

## 学校Chromebookでの公開（Linux不要）
1. 学校のルールを確認。GitHub / Firebaseへのアクセスが許可されている場合のみ進めます。学校用アカウントや児童の個人情報は使わないでください。
2. https://console.firebase.google.com/ で個人のGoogleアカウントから無料枠（Spark）プロジェクト作成。
3. Firebase Authentication → ログイン方法 → 匿名 を有効化。
4. Realtime Database を作り、Rulesに `database.rules.json` の全文を貼り付けて**公開**。ルールは身内向け試作のため公開・第三者利用には不十分です。Database URLを控える。
5. Firebaseプロジェクトの「Webアプリを追加」で設定値を取得し、`firebase-config.js` の `REPLACE_ME` を含む設定項目を正しい値に置き換えます（`databaseURL` も必要）。
6. https://github.com/ に個人アカウントでログイン → New repository（Public）→ "charge-attack" → Create。
7. GitHubの Add file → Upload files で **このフォルダの中身** `index.html`, `app.js`, `firebase-config.js`, `assets/` の各画像をアップロード。フォルダを維持します（Web UIでフォルダのアップロードが難しい場合、1枚ずつ `assets/ファイル名` として作成する方法があります）。`README.md` と rules はゲーム公開に必須ではありません。
8. Settings → Pages → Deploy from a branch → main / (root) → Save。
9. 数分後、`https://ユーザー名.github.io/charge-attack/` などのURLにアクセス。端末2台からルーム参加テスト。

## 注意
- 画面デザインのモック画像は「背景カード画像」として使用します。ユーザーが操作するボタン、数字、対戦状況はHTMLとFirebaseが管理します。
- ルーム内の他者による不正書き込みを完全に防ぐ安全な作りではありません。見知らぬ人に広く公開するサービスとしては使わないでください。
- 友達が途中退出した場合の再接続処理は簡易版です。同じタブを維持してください。
- データベースに勝敗やチャージ数が保存されます。名前や住所などの個人情報を入力しないでください。
- FirebaseのWeb設定値は秘密鍵ではありませんが、セキュリティルールは必須です。
- 学校管理Chromebookでサイトやログインが制限されるときは、管理者の許可を求めるか個人端末で公開してください。制限を回避しないでください。
