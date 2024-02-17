# japansese-reasoning-datasets

推論タスクには、数学推論/常識推論/記号推論の 3 つがある。

プロンプトエンジニアリングでは、各タスクごとにデータセットを選び、モデルの性能を評価している。

- [数学推論の評価](https://scrapbox.io/evergreens/%E6%95%B0%E5%AD%A6%E6%8E%A8%E8%AB%96%E3%82%BF%E3%82%B9%E3%82%AF%E3%82%92%E3%81%A9%E3%81%86%E8%A9%95%E4%BE%A1%E3%81%99%E3%82%8B%E3%81%8B%EF%BC%9F)
- [常識推論の評価](https://scrapbox.io/evergreens/%E5%B8%B8%E8%AD%98%E6%8E%A8%E8%AB%96%E3%82%BF%E3%82%B9%E3%82%AF%E3%82%92%E3%81%A9%E3%81%86%E8%A9%95%E4%BE%A1%E3%81%99%E3%82%8B%E3%81%8B%EF%BC%9F)
- [記号推論の評価](https://scrapbox.io/evergreens/%E8%A8%98%E5%8F%B7%E6%8E%A8%E8%AB%96%E3%82%BF%E3%82%B9%E3%82%AF%E3%82%92%E3%81%A9%E3%81%86%E8%A9%95%E4%BE%A1%E3%81%99%E3%82%8B%E3%81%8B%EF%BC%9F)

しかし一方で、プロンプトエンジニアリングでは、推論タスクの性能を上げるプロンプトを探求する場合、どれか一つの推論能力を見たいというケースは少ない。

1 つのプロンプトの修正に対し、3 つの推論タスクを同時に評価したいというニーズがある。
また、モデルの性能と違い、元データをそのまま使うと、コスト(API 費用、時間)がかかりすぎるという課題もある。

そこで、それぞれの推論タスクから、5-10 問ずつピックアップして、推論評価のための統合したデータセットを作る。

なお、各データセットは問題形式が若干異なる。そのため、元データを調整し、5 つの問題から 1 つの選択を選ぶ選択問題に統一する。

## test1.json

以下の問題を混ぜたデータセット

- [MMLU: elementary-math](https://github.com/nlp-waseda/JMMLU/blob/main/JMMLU/elementary_mathematics.csv): 5 問
- [MMLU: high-school-math](https://github.com/nlp-waseda/JMMLU/blob/main/JMMLU/high_school_mathematics.csv): 5 問
- [JCommonsenseQA](https://github.com/nlp-waseda/chain-of-thought-ja-dataset/blob/main/dataset/jcommonsenseqa/test.json): 5 問
- [Last Letter Concatenation](https://github.com/nlp-waseda/chain-of-thought-ja-dataset/blob/main/dataset/last_letter_connection/test.json): 5 問

### 結果

https://chainforge.ai/play/?f=3fni6zh8jwmc4
![alt text](<CleanShot 2024-02-17 at 10.06.21.png>)

モデル: GPT-3.5-Turbo-1106
temperature:0

正解率 80%であった

## test2.json

test1.json の数学タスクを、小学生->大学に変更したもの
データの内訳は、以下の通り

- [MMLU: high-school-math](https://github.com/nlp-waseda/JMMLU/blob/main/JMMLU/high_school_mathematics.csv): 5 問
- [MMLU: college-math](https://github.com/nlp-waseda/JMMLU/blob/main/JMMLU/college_mathematics.csv): 5 問
- [JCommonsenseQA](https://github.com/nlp-waseda/chain-of-thought-ja-dataset/blob/main/dataset/jcommonsenseqa/test.json): 5 問
- [Last Letter Concatenation](https://github.com/nlp-waseda/chain-of-thought-ja-dataset/blob/main/dataset/last_letter_connection/test.json): 5 問

### 結果

https://chainforge.ai/play/?f=p74iexgsysvy
![alt text](<CleanShot 2024-02-17 at 10.51.37.png>)
モデル: GPT-3.5-Turbo-1106
temperature:0

正解率 60%であった

## test3.json

test1, test2.json の結果から、間違えた問題だけを厳選したタスク
API の費用が気になったり、難しい問題を解かせたいときに有効なデータセット
データの内訳は、以下の通り

- [MMLU: high-school-math](https://github.com/nlp-waseda/JMMLU/blob/main/JMMLU/high_school_mathematics.csv): 2 問(test1.json id=9,10)
- [MMLU: college-math](https://github.com/nlp-waseda/JMMLU/blob/main/JMMLU/college_mathematics.csv): 4 問 (test2.json id=6,7,8,10)
- [Last Letter Concatenation](https://github.com/nlp-waseda/chain-of-thought-ja-dataset/blob/main/dataset/last_letter_connection/test.json): 2 問(test1.json id=19,20)

### 結果

https://chainforge.ai/play/?f=1xaarqota7skd
![alt text](<CleanShot 2024-02-17 at 11.06.56.png>)
モデル: GPT-3.5-Turbo-1106
temperature:0

正解率 13%であった

## データと ChainForge の使い方

- step1.
  使いたいデータ(test{number}.json)の ChainForge の url をクリックしてください。

- step2.
  Tabular Data Node に、json ファイルが import されていて、このまま使えます。プロンプトを実行するときは、PromptNode の再生ボタンをクリックしてください。
  ![alt text](<CleanShot 2024-02-17 at 11.09.39.png>)

- step3.
  実行結果を確認するときは、Simple Evaluator の再生ボタンを押してください。グラフが表示されたら、y-axis の値を変更すれば、別の視点からグラフを分析できます。

![alt text](<CleanShot 2024-02-17 at 11.10.39.png>)
