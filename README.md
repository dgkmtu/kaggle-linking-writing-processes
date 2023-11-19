# kaggle-linking-writing-processes
Linking Writing Processes to Writing Quality コンペのリポジトリ

- directory tree
```
Kaggle-Cornell-Birdcall-Identification
├── README.md
├── data         <---- gitで管理するデータ
├── nb           <---- jupyter lab で作業したノートブック
└── src          <---- 参考にしたのノートブック

```

## Memo
- term
  - nb: ノートブック

## Basics
**Overview(Google Translate)**
このコンテストの目的は、全体的な文章の品質を予測することです。タイピング動作はエッセイの結果に影響しますか? 書き込みプロセスの特徴をキャプチャしたキーストローク ログの大規模なデータセットでトレーニングされたモデルを開発します。  

あなたの研究は、学習者の作文行動と作文パフォーマンスの関係を調査するのに役立ち、作文指導、自動作文評価技術の開発、インテリジェントな個別指導システムに貴重な洞察を提供する可能性があります。

## Log
### 20231101
- メモ作成開始
- [Writing Quality](https://www.kaggle.com/code/klyushnik/writing-quality/notebook)
- まずは、このnotebookを写経して流れを確認しよう。
- これまでkaggleカーネルで作っていたけど、Google Driveに移した。
- Overviewの訳をREADMEファイルに追加した。
- Discussionを見てみた。submissionがfailしただけでも、コメントしてる人がいるね。
- nb01_writing_quality.ipynb
- notebookはDrop Nanまで完了
- 次はBaselineだね。モデルを作って最後にsubmitまでいく流れだね。

### 20231102
nb01
- Baselineの写経
- Google Coraboratryはcatboostはpipしないといけないんだね。
- Baselineの写経完了
- 次はData preparationの節
- Data preparationの写経完了
- 次はSplit and Trainの節
- ここで各モデルのベストパラメータを見つけているんだね。

Discussion
- [Probably a small bug in the training data](https://www.kaggle.com/competitions/linking-writing-processes-to-writing-quality/discussion/452264)
- データにおかしなところがあると書いてある。明日試しに確認してみようかな。
- このコメントに返信しようかな「確かに不自然な動きに見えます。他のレコードも確認すべきでしょうか？それとも、誤差として容認すべきでしょうか？」これを訳しますかね。
- Discussionを見ていると、データ内容の解釈にも役立つかもね。

### 20231103
nb01
- 各モデルの最適パラメータの探索
- LightBGMのearly_stoppingの仕様が違うらしいね。
- [LightGBMのearly_stoppingの仕様が変わったので、使用法を調べてみた](https://qiita.com/c60evaporator/items/2b7a2820d575e212bcf4)
- first submit実施
- internet connectionを切断したり、設定が面倒だったね。

Discussion
- [Link Writing Simple LGBM baseline](https://www.kaggle.com/code/hengzheng/link-writing-simple-lgbm-baseline)
- 次はこのnotebookを参考にしてみようかな。
- コメントしてみた。
- https://www.kaggle.com/competitions/linking-writing-processes-to-writing-quality/discussion/451081#2510956
- 本当にくだらないコメントだけど、これからDiscussionに慣れていこう。

### 20231104
nb02
- [Easy Feature Analysis](https://www.kaggle.com/code/junjitakeshima/wrtqlty-easy-feature-analysis-eng)
- このnotebookを写経してみよう。日本人の方のnotebookかつ、説明もしっかりしているので、参考になりそう。
- 日本語の人のnotebookを写経すると、理解度は段違いだね。
- 簡単なモデル計算でもいろんなことが分かるんだね。
- エッセイの文字数が多いと、スコアに大きく響く傾向
- down_timeが小さいほど、つまり取り掛かる時間が早い程、スコアが良く
- up_timeが大きいほど、つまりエッセイが完成する時間が遅い程、スコアが良い。
- まあ、色々見ていると、エッセイの中身をどれだけデータに入れるかが鍵になりそうだね。

### 20231106
- 今日で写経2回目は完了になるかな〜
- 次はessayの難易度を統合して、submitしてみよう。
- nb03ではnb01とnb02を統合してsubmitする。
- その前にnb01及びnb02の前処理について整理しよう。
- nb01
- summary_time : エッセイを書き上げるまでの合計時間
- start_pause : エッセイを書き始めた時間
- enter_click : Enterキーをクリックした回数
- space_click : Spaceキーをクリックした回数
- backspace_click : Backspaceキーをクリックした回数
- symbol_length : エッセイを書き上げた時点のカーソル位置
- text_length : エッセイの文字数
- nonproduction_feature : 入力がない場合の動作の割合
- input_feature : 入力がある場合の動作の割合
- remove_feature : 削除する動作の割合
- mean_action_time : 動作時間の平均
- replace_feature : Replaceの動作をした回数
- text_change_unique : 文章を変えたユニーク数
- sentence_size_feature : 1文の長さ

### 20231107
- nb02の前処理を書き出そうかな。
- 処理が共通するものは、名前を統一しよう
- nb02
- (共通)start_pause : エッセイを書き始めた時間
- end_pause : エッセイを書き終えた時間
- (共通)mean_action_time : 動作時間の平均
- sum_action_time : 動作時間の合計
- max_action_time : 動作時間の最終時間
- (共通)text_length : エッセイの文字数
- text_length_mean : エッセイの文字列の平均(空白行も含めているので微妙な変数)
- (共通)symbol_length : エッセイを書き上げた時点のカーソル位置
- symbol_length_mean : カーソル位置の平均
- Inpu : input処理をしたときのフラグ
- Move : input処理をしたときのフラグ

- nb01とnb02の統合をやってみたけど、何も考えずにやってしまうと上手くいかないね〜
- 文書をdecodeする過程で少し操作しているみたいだ。
- 変数がややこしすぎて混乱したので、もう一度冷静になって明日考え直してみよう。

### 20231108
- nb03
- nb02のtext_change関数から統合する
- やはりテストデータになると、エッセイ難易度がうまく反映されていないな
- nb02の元のnotebookとさらに元のnotebookを確認するか
- 元のnotebookを確認したら、こちらもエッセイ難易度がうまく反映されていない
- 元の元のnotebookを確認するしかないね〜
- ただし、その前にこっちのnotebookを統合して進みましょうか。nb04を新規作成
[Link Writing Simple LGBM baseline](https://www.kaggle.com/code/hengzheng/link-writing-simple-lgbm-baseline)

### 20231109
nb05
- nb01とnb04を統合してnb05を作成する。
- 特徴量の作成はnb04に従い、学習はnb01の方法に従う。
- 計算かなりかかりそうだね〜GPU使わないといけないかな〜

### 20231110
nb05
- RAM満杯になっちゃって、接続しなおしちゃうのか
- 無駄な変数とかを消去する工夫をしないとかな
- 2回目のsubmission
- Public Scoreは0.634で648位か〜
- まあ、もうちょい改善できる点はあるので、少しnb01とnb04の統合を進めよう。
- 欠損値消去をやってみようかね
- [Towards TF-IDF in logs features](https://www.kaggle.com/code/olyatsimboy/towards-tf-idf-in-logs-features)
- 次はこのnotebookを参考にしよう。

### 20231113
nb06
- 写経の続き
- Google ColaboratryのシステムRAMが溢れてしまうな〜
- EDAをコメントアウトしたら、なんとか処理できた。
- まあ、処理は続けられそう。
- Kaggleで勝つでKFoldの箇所を少しみた。処理としては計算時間がかかりそうだね〜少し簡単なモデルを作ってみるかな。

### 20231114
nb06
- 写経の続き
- 写経は今日で完了しそうだね。KFoldの構造はなんとなく理解できてきたぞ。
- nb06のsubmissionまでいこう。
- [LGBM and NN on sentences](https://www.kaggle.com/code/alexryzhkov/lgbm-and-nn-on-sentences)
- このノートブックのスコアが良かったとのこと
- nb07ではこのノートブックの写経を次にしてみようかな。
- おおっnb06のスコアが0.603で最高だった。
- よく分からんなあ〜これでいけるのか。nb01,nb04,nb06を整理したい。

### 20231115
nb07
- 写経を始める。
- 対象は[LGBM and NN on sentences](https://www.kaggle.com/code/alexryzhkov/lgbm-and-nn-on-sentences)
- essayを連結した情報も使用するんだね。
- これまでの情報の統合みたいなノートブックかなぁ。

### 20231120
- 以下2つのNotebookを統合して、結果を比較してみた。
- [LGBM and NN on sentences](https://www.kaggle.com/code/alexryzhkov/lgbm-and-nn-on-sentences)
- [Feature Engineering: Sentence & paragraph features](https://www.kaggle.com/code/hiarsl/feature-engineering-sentence-paragraph-features/notebook)
- これを統合してみると、前処理は同じことをしていてモデリングの違いのみになっている。
- 新たに、スコアの良い結果が[LB 0.585 New best public score!](https://www.kaggle.com/competitions/linking-writing-processes-to-writing-quality/discussion/456395)のコメントが出てきた。
- これをまずは動かしてみて、中身をみてみようかな。