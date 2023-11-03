# kaggle-linking-writing-processes
Linking Writing Processes to Writing Quality コンペのリポジトリ

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