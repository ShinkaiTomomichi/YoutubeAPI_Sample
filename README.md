# get_hololive_videos

ホロライブに関連する動画情報をYoutube Data APIを利用して取得するサンプルです

## 内容

### input
各VtuberのチャンネルIDの一覧です

- `hololive_channels`: ホロライブの全VtuberのチャンネルIDの一覧（2021/11現在）
- `okakoro_channels.csv`: 戌神ころね, 猫又おかゆのチャンネルIDの一覧

`okakoro_channels.csv`はYoutube Data APIの利用上限超過を回避する際に利用します

### secret
Youtube Data APIを利用する際は、APIキーをテキスト化したファイルを、このディレクトリ内に`apikey`というファイル名で保存してください

### get_videos
各チャンネルから投稿された動画全てに対し以下の情報を取得し、`output/<okakoro or hololive>/<チャンネル名>.csv`に保存します

| データ | 詳細 |
| ---- | ---- |
| Id | 動画のIDです。APIで詳細な動画情報を取得する際に利用します。 |
| Name | 配信者の名前です。|
| ChannelId | チャンネルのIDです。APIで詳細なチャンネル情報を取得する際に利用します。 |
| Date | 動画の投稿日時です。 |
| Title | 動画のタイトルです。 |
| Thumbnail | 動画のサムネイル画像のリンクです。 |
| CategoryId | 動画のカテゴリです。 |
| Duration | 動画の再生時間です。 |
| DurationOriginal | 変換前（ISO表記）の動画の再生時間です。 |
| Description | 動画の概要欄です。稀に概要欄が設定されていない動画がある場合、NULLになります。 |
| ViewCount | 動画の再生数です。動画の公開設定次第では取得できない場合があります。 |
| LikeCount | 動画の高評価数です。動画の公開設定次第では取得できない場合があります。|
| DislikeCount | 動画の低評価数です。動画の公開設定次第では取得できない場合があります。 |
| CommentCount | 動画のコメント数です。動画の公開設定次第では取得できない場合があります。 |

### annotation_song_videos
`classify_videos`で利用するため、`get_videos`で取得したデータにアノテーションします

今回は人力で以下の方法で歌動画と非歌動画を分類します
1. 動画時間が歌っぽくない動画をスクリーニングし`unlabeled`に保存
1. サムネイル画像を見ながら人力でlabel_0, label_1ディレクトリに格納
1. 格納された画像を元に訓練データを再作成

### classify_videos
`get_videos`, `annotation_song_videos`で取得したデータを元に歌動画と非歌動画の分類を行います

分類には簡単なLASSOモデルを利用しています

### get_comments
`suggest_videos`で利用するため、`annotation_song_videos`で取得したデータのコメント情報を取得します

### suggest_videos
`get_comments`で取得したコメントの共起量をベースに動画の推薦を行います

## 参考
- [API Reference](https://developers.google.com/youtube/v3/docs)

- [Youtube Data APIを使ってPythonでYoutubeデータを取得する](https://qiita.com/g-k/items/7c98efe21257afac70e9)
