# 🚗 JDM Kei-Car Market Analysis in the USA
**Exploring the massive "Kei" vehicle data from Craigslist (1.4GB Dataset)**

アメリカの中古車サイト「Craigslist」の膨大なデータ（約1.4GB）を解析し、日本独自の規格である「軽自動車」がアメリカでどのように流通しているかを調査したプロジェクトです。

## 🌟 Key Findings (主な発見)
- **Massive Scale**: 1.4GBの生データから約26,000台の軽乗用車を抽出。
- **Dominant Model**: **DAIHATSU MOVE** が圧倒的な流通量を誇り、アメリカでの「JDM実用車」としての地位を確立している。
- **The "Tanto" Anomaly**: 本来「25年ルール」で輸入できないはずの **DAIHATSU TANTO** が300台以上見つかるという、データ上の異常事態（アノマリー）を発見。

## 🛠️ Technical Challenges (乗り越えた壁)
- **Data Cleansing**: 1.4GBの巨大なCSVに含まれる「広告文」や「壊れた行」を、Pandasの技術（skiprows, on_bad_lines, engine='python'等）を駆使して修正・読み込み。
- **Filtering**: 軽トラ（Truck）以外の「軽乗用車」に特化するため、モデル名や排気量（660cc）に基づく高度なフィルタリングを実装。

## Files
- `jdm_kcar_sample.csv`: 抽出したデータの1000件分サンプル
- `mystery_tanto_list.csv`: 解禁前の謎を追うためのタント専用リスト
- `main.py`: 1.4GBの巨人を手なずけた解析スクリプト

##  Author
- **Buddy (Learning Data Science)**
- 昔タントに乗っていた経験から、アメリカにおける日本の軽自動車の可能性を追跡中！

### 🕵️‍♂️ Case Study: The "Tanto" Anomaly
当初、データから365台の **DAIHATSU TANTO** を検出しましたが、詳細な分析（Data Drilling）により以下の事実が判明しました。

- **仮説**: 25年ルールを潜り抜けて大量のタントが輸入されている？
- **検証**: 説明文（Description）を精査したところ、"Daihatsu" という車名の記載はゼロ。
- **結論**: すべてスペイン語の定型文 **"en tanto"**（〜の間、その一方で）を誤検知した「偽陽性（False Positive）」であったことが判明。

この結果を受け、モデル名だけでなく「メーカー名」や「キーワード」を組み合わせた、より精度の高いフィルタリングを実装しました。

## 🕵️‍♂️ Key Findings: The "Fake" JDM Market
巨大なデータセットからダイハツの軽自動車を抽出した際、非常に興味深い「偽陽性（False Positive）」の事例が見つかりました。

### 1. The Tanto Mystery (タントの謎)
- **Initial Count:** 365 units
- **Truth:** **0 units**
- **Reason:** 全てがスペイン語の挨拶や接続詞である **"en tanto"** を誤検知していました。カリフォルニアやフロリダなどのスペイン語圏の投稿が多いために発生したノイズです。

### 2. The Move Myth (ムーヴの神話)
- **Initial Count:** 14,850 units
- **Truth:** **0 units**
- **Reason:** 全てが中古車販売の決まり文句である **"Ready to move"**（即納車可能）や **"Moving sale"**（引っ越し売り切り）を検知していました。

## 💡 What I Learned (学んだこと)
- **Data Cleaning is Crucial:** 単純なモデル名だけの検索がいかに危険かを学びました。
- **Context Matters:** 言語の壁（スペイン語）や業界用語（販売文句）がデータにどう影響するかを実体験しました。
- **Real JDM Scarcity:** 1.4GBのデータを持ってしても「本物の軽自動車」を見つけるのは極めて困難であり、アメリカ市場におけるJDMの希少性が改めて浮き彫りになりました。
