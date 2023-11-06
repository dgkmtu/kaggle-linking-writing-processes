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

