# get_hololive_videos

ホロライブに所属するVTuberの動画情報をYoutube Data APIを利用して取得します

## 内容

### input
各VtuberのチャンネルIDの一覧です

- `hololive_channels`: ホロライブの全VtuberのチャンネルIDの一覧
- `okakoro_channels.csv`: 戌神ころね, 猫又おかゆのチャンネルIDの一覧

`okakoro_channels.csv`はYoutube Data APIの利用上限超過を回避する際に利用します

### secret
利用時にはこのディレクトリ内にYoutube Data APIを利用するためのAPIキーを`apikey`というファイル名で保存してください

### get_videos
各チャンネルから以下の情報を取得し、`output/<okakoro or hololive>/<チャンネル名>.csv`に保存します

| データ | 詳細 |
| ---- | ---- |
| Id | 動画のIDです。APIで詳細な動画情報を取得する際に利用します。 |
| Name | VTuberの名前です。|
| ChannelId | チャンネルのIDです。APIで詳細なチャンネル情報を取得する際に利用します。 |
| Date | 動画の投稿日時です。 |
| Title | 動画のタイトルです。 |
| Thumbnail | 動画のサムネイル画像のリンクです。 |
| CategoryId | 動画のカテゴリです。 |
| Duration | 動画の再生時間です。 |
| Duration | 変換前（ISO表記）の動画の再生時間です。 |
| Description | 動画の概要欄です。 |
| Viewcount | 動画の再生数です。動画の公開設定次第では取得できない場合があります。 |
| LikeCount | 動画の高評価数です。動画の公開設定次第では取得できない場合があります。|
| DislikeCount | 動画の低評価数です。動画の公開設定次第では取得できない場合があります。 |
| CommentCount | 動画のコメント数です。動画の公開設定次第では取得できない場合があります。 |

### annotation_videos
`get_videos`で取得したデータにアノテーションします

1. 動画時間でフィルタリングし`unlabeled`に保存
1. サムネイル画像を見ながら分類
1. label_0, label_1に格納された画像を分類

### classify_videos
`get_videos`で取得したデータから歌動画の抽出を試みます

### get_comments
`classify_videos`

### suggest_videos
`get_comments`で取得したコメントをベースに動画の推薦を試みます


## 参考
- [API Reference](https://developers.google.com/youtube/v3/docs)

- [Youtube Data APIを使ってPythonでYoutubeデータを取得する](https://qiita.com/g-k/items/7c98efe21257afac70e9)
