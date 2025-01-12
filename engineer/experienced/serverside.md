# Nextremer プログラミング課題 (選考用)

# 課題の目的
Webアプリケーション開発に関する基礎的なスキル、基礎的なドキュメンテーションのスキルを持っているかどうかを確認させて頂くためのプログラミング課題です。  

# タスク
1. 本ドキュメントで指定する仕様のWebアプリを開発しインターネットへ公開
    - 有料サービスを使う必要はないため Fly.io等 の無料枠等をご利用ください
    - Webアプリへのアクセスにはパスワード認証をかけて頂いても構いません
2. 以下をご自身の GitHub リポジトリで公開
    - ソースコード
        - APIキーなどの秘密情報は含めないようにご注意ください
    - システム構成図
        - 全体の構成を説明する図を作成し画像をリポジトリにコミットしてください
        - 図のフォーマットは問いません

# Webアプリ仕様
Botとのチャットアプリケーションを実装して頂きます。  
ここで指定されていない仕様についてはご自由に設計を考えて実装してください。

## サーバーサイド
Botの応答はサーバーサイドの処理で生成してください。  
リクエスト・レスポンスをJSON形式で処理するAPIとして実装してください。  
またデータの保存にはデータベースを利用してください。

### 使用言語、フレームワーク、バージョン
以下のどちらかの言語を選んで実装して頂きます。

- TypeScipt
- Python

### APIインターフェース仕様

#### 1. Botとの会話
Botの応答文字列を生成し返却します。  
応答したデータの履歴をデータベースに保存します。  

##### URL

```
POST /chat
```
##### Request
```
{
  "user_input": "こんにちは" // ユーザーが入力した文字列
}
```

##### Response
```
{
  "user_input": "こんにちは", // ユーザーが入力した文字列
  "bot_response": "こんにちは。", // Botが応答した文字列
  "response_timestamp": "2018-04-10T03:50:40" // リクエストを返した時刻(日本標準時)
}
```

##### Botの応答パターン
Botの応答を以下の3種類実装してください。  
以下で指定したユーザー入力にのみ応答するよう実装して頂ければ構いません。  
また、ユーザー入力の表記の揺れに対応する必要はありません。  

1. 固定応答
    - ユーザー入力: こんにちは
    - Bot応答: こんにちは。
2. 現在時刻
    - ユーザー入力: 今何時？
    - Bot応答: 10時10分です。
        - リクエストを受け付けた時点の現在時刻(JST)を応答すること
3. 天気
    - ユーザー入力: 今日の東京の天気は？
    - Bot応答: 晴れです。
        - 天気情報の取得は何らかのWebAPIを利用して取得すること  
        - "晴れ", "雨", "曇り" など天気についての文言は自由
            - 例：APIのレスポンスが `cloudy` だった場合、表示する結果は "曇り" でも "曇天" でも特に問題はないという意味です


#### 2. 履歴一覧の取得
過去に応答したデータの履歴をデータベースより取得し返却します。  

##### URL

```
GET /history/list
```
##### Request
リクエスト時のパラメータは無し

###### Response
最新のものから10件配列で返却  
配列内のデータは `response_timestamp` の降順でセットされていること  
```
[
  {
    "user_input": "今日の東京の天気は？",
    "bot_response": "晴れです。",
    "response_timestamp": "2018-04-10T04:50:40"
  },
  {
    "user_input": "今何時？",
    "bot_response": "3時40分です。",
    "response_timestamp": "2018-04-10T03:40:30"
  },
  {
    "user_input": "こんにちは",
    "bot_response": "こんにちは。",
    "response_timestamp": "2018-04-10T02:30:20"
  },
  ...
]
```

## フロントエンド
フロントエンド側からサーバーのAPIにアクセスします。  
画面の入出力項目はこちらを満たすように実装してください。  
デザイン、レイアウトの質は問わないため最低限のもので構いません。  
ここで指定されていない仕様についてはご自由に実装してください。  

![画面イメージ](https://raw.githubusercontent.com/Nextremer/recruitment-examination/master/img/view_image.jpg)

### 使用言語、フレームワーク、バージョン
フロントエンドは `React.js` を利用して実装をお願いします。

# 評価する観点
以下の観点で評価させて頂きます。
- 公開されているWebアプリが指定した仕様の通りに動作するか
- 指定した仕様の通りに機能が実装されているか
- システム構成図で全体が表現できているか

# ご提出いただくもの
- 本課題のソースコードがコミットされているGitHubリポジトリのURL
- 公開されているWebアプリのURL
  - Webアプリは弊社からの連絡があるまでは公開した状態としておいてください。
    - ご提出頂いてから5営業日以内にご連絡します。
  - パスワード認証を設定している場合はパスワード情報も併せてご提出ください。  

# 課題に関する質問がある場合
本プログラミング課題に関するご質問がある場合は以下のメールアドレスまでご連絡ください。  
recruit@nextremer.com 

