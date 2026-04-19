# HISTORY

## 2026-04-19

### バグ修正: OAuth2 クライアントに client_id/client_secret を渡すように修正

**問題**: `new google.auth.OAuth2()` に client_id と client_secret を渡していなかったため、アクセストークン（有効期限1時間）が切れた際に googleapis ライブラリが自動リフレッシュできずAPIエラーが発生していた。

**修正**: `gcp-oauth.keys.json` から client_id と client_secret を読み込み、`OAuth2` コンストラクタに渡すように変更。

### 機能追加: トークン更新時の自動保存

**内容**: OAuth2 クライアントの `tokens` イベントを監視し、アクセストークンが更新された際に自動的に credentials ファイルへ書き戻すようにした。これにより MCP サーバーを再起動せずともトークンが継続的に有効な状態を保てる。

### 機能追加: 認証エラー時のわかりやすいエラーメッセージ

**内容**: ツール呼び出し時に認証エラー（invalid_grant / invalid_request / 401）が発生した場合、MCP エラーレスポンスとして再認証手順を含むメッセージを返すように変更。Claude Code 上でエラー原因と対処法が即座にわかるようになった。
