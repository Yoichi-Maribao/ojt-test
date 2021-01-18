# 卒業テストデバッグ内容
[x] ログイン画面に遷移できない

→config/routes.rb内のdevise_forとresources :userの記述を逆にすることで解決

deviseを先に記述しないとエラーがおこる

[x] ログイン、サインアップできない
エラー内容
___
### 3 errors prohibited this user from being saved:
-Name can't be blank

-Name is too short (minimum is 2 characters)

-Introduction can't be blank

___
-名前を正しく入力しているのにもかかわらず正しく送信されない

→:nameパラメータの送信を許可するために、app/controllers/application_controller.rb内のconfigure_permitted_parametersメソッドにて:keysに:nameを追加

-Introductionに不要なバリデーションが当たっている

→app/models/user.rb内でintroductionのバリデーション記述部からpresence: trueを削除

[x] 画像が反映されない

→app/models/user.rb内でattachment以下の記述を :profile_imageに変更（末尾の_idを削除）

[x] 本の投稿ができない

→user.idがnilだったため、app/controllers/books_controller.rbのcreateアクション内にて@new_book.user_id = current_user.idと追記

[x] 本の編集画面でエラーが出る

→app/controllers/books_controller.rbのeditアクション部で全角スペースが混じっていたためうまく読み込まれずエラーが起きていた

[x] 本の削除ができない

→books_controllerのdestroyメソッド内でdestroyがdestryとタイポされていた。

[x] エラーメッセージが出ない

→createアクション、updateアクション内での処理に失敗した際の分岐がrenderではなくredirectになっていた。

[x] 本の一覧ページから詳細ページへのリンク先が適切ではない

→index内の本のタイトルから詳細へ飛ぶ際のパス指定がbook_pathではなくbooks_pathになっていた（showではなくindexへのパス。)
