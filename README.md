# get_hololive_videos

ホロライブに所属するVTuberの動画情報をYoutube Data APIを利用して取得します

## 内容

### input
各VtuberのチャンネルIDの一覧です

- `hololive_channels`: ホロライブの全VtuberのチャンネルIDの一覧
- `okakoro_channels.csv`: 戌神ころね, 猫又おかゆのチャンネルIDの一覧

サンプルコードではYoutube Data APIの利用上限超過を回避するために、サイズの小さい`okakoro_channels.csv`を利用します

### secret
利用時にはこのディレクトリ内にYoutube Data APIを利用するためのAPIキーを`apikey`というファイル名で保存してください

### get_hololive_videos
各チャンネルから動画情報を取得し、`output/okakoro/<チャンネル名>.csv`に保存します

今回格納した情報は下記になります

| データ | 詳細 |
| ---- | ---- |
| Id | 動画のIDです。APIで詳細な動画情報を取得する際や動画へアクセスする際に利用します。 |
| Channel | チャンネルのIDです。APIで詳細なチャンネル情報を取得する際や動画へアクセスする際に利用します。 |
| Date | 動画の投稿日時を取得します。 |
| Title | 動画のタイトルを取得します。 |
| Thumbnail | 動画のサムネイル画像のリンクです。 |
| CategoryId | 動画のカテゴリを取得します。 |
| Duration | 動画の再生時間を取得します。 |
| Description | 動画の概要を取得します。 |
| Viewcount | 動画の再生数を取得します。 |
| LikeCount | 動画の高評価数を取得します。動画の公開設定次第では取得できない場合があります。 |
| DislikeCount | 動画の低評価数を取得します。動画の公開設定次第では取得できない場合があります。 |
| CommentCount | 動画のコメント数を取得します。動画の公開設定次第では取得できない場合があります。 |

### get_hololive_ranking
`get_hololive_videos`で取得したデータからランキングを生成します

### get_hololive_songs_1
`get_hololive_videos`で取得したデータから歌動画の抽出を試みます

### get_hololive_songs_2
歌動画の抽出に機械学習を利用してみます（作成途中です）

## 参考

- [YouTube のヘルプ コミュニティ](https://support.google.com/youtube/community?hl=ja)

- [API Reference](https://developers.google.com/youtube/v3/docs)

- [Youtube Data APIを使ってPythonでYoutubeデータを取得する](https://qiita.com/g-k/items/7c98efe21257afac70e9)

- [Youtube API v3 動画カテゴリIDリスト](https://qiita.com/nabeyaki/items/c3d0421538c8faacb130)

- [YouTube Data API v3を試してみました](https://phpjavascriptroom.com/?t=strm&p=youtubedataapi_v3_list)