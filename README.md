# japansese-reasoning-datasets

推論タスクには、数学推論/常識推論/記号推論の 3 つがある。

プロンプトエンジニアリングでは、各タスクごとにデータセットを選び、モデルの性能を評価している。

- [数学推論の評価](https://scrapbox.io/evergreens/%E6%95%B0%E5%AD%A6%E6%8E%A8%E8%AB%96%E3%82%BF%E3%82%B9%E3%82%AF%E3%82%92%E3%81%A9%E3%81%86%E8%A9%95%E4%BE%A1%E3%81%99%E3%82%8B%E3%81%8B%EF%BC%9F)
- [常識推論の評価](https://scrapbox.io/evergreens/%E5%B8%B8%E8%AD%98%E6%8E%A8%E8%AB%96%E3%82%BF%E3%82%B9%E3%82%AF%E3%82%92%E3%81%A9%E3%81%86%E8%A9%95%E4%BE%A1%E3%81%99%E3%82%8B%E3%81%8B%EF%BC%9F)
- [記号推論の評価](https://scrapbox.io/evergreens/%E8%A8%98%E5%8F%B7%E6%8E%A8%E8%AB%96%E3%82%BF%E3%82%B9%E3%82%AF%E3%82%92%E3%81%A9%E3%81%86%E8%A9%95%E4%BE%A1%E3%81%99%E3%82%8B%E3%81%8B%EF%BC%9F)

しかし一方で、プロンプトエンジニアリングでは、推論タスクの性能を上げるプロンプトを探求する場合、どれか一つの推論能力を見たいというケースは少ない。

1 つのプロンプトの修正に対し、3 つの推論タスクを同時に評価したいというニーズがある。
また、モデルの性能と違い、データ量をそのまま使うと、コスト(API 費用、時間)がかかりすぎるという問題もある。

そこで、それぞれの日推論タスクから、5-10 問ずつピックアップして統合したデータを作る。

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
