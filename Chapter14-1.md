---
marp: true
math: mathjax
header: "ESL輪読"
paginate: true
style: |
  strong {
    color: #F79428;
  }
  em {
    font-style: normal;
    color: #0B3E8D;
    font-weight: bold;
  }
  h1 {
    color: #0B3E8D;
  }
  h2 {
    color: #0B3E8D;
    margin-bottom:-.2em;
  }
  h2 strong {
    color: chocolate;
  }
  h3 {
    margin-bottom:-.1em;
  }
  h3 strong {
    color: chocolate;
  }
  .columns {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1rem;
  }
  .columns.var {
    display: grid;
    grid-template-columns: var(--ratio) 1fr;
    gap: 1rem;
  }
  .columns.spaced {
    display: grid;
    grid-template-columns: var(--ratio) 10% 1fr;
    gap: 1rem;
  }
  .gray {
    background: whitesmoke;
  }
  .theorem {
    background: whitesmoke;
    padding-top: 0.1em;
    padding-bottom: 0.1em;
    padding-left: 0.4em;
  }
  .statement {
    margin-top: -0.5em;
    padding-left: 0.7em;
  }
  .quote {
    background: whitesmoke;
    margin-left: 5%;
    margin-right: 5%;
    margin-bottom: 3%;
  }
  .quote.white {
    background: white;
  }  .katex .delimcenter,
  .katex .op-symbol {
    display: inline-block;
  }  
  .arrow {
    margin-top: auto;
    margin-bottom: auto;
    margin-left: auto;
    margin-right: auto;
    width: 0; 
    height: 0;   
  }
  .arrow.right {
    border-top: 40px solid transparent;
    border-bottom: 40px solid transparent;
    border-left: 40px solid gray;
  }
  .arrow.down {
    border-left: 40px solid transparent;
    border-right: 40px solid transparent;
    border-top: 40px solid gray;
  }
  .arrow.up {
    border-left: 40px solid transparent;
    border-right: 40px solid transparent;
    border-bottom: 40px solid gray;
  }
  .center {
    margin-right: auto;
    margin-left: auto;
    text-align: center; 
  }
  .middle {
    margin-top: auto;
    margin-bottom: auto;
  }
  .large {
    font-size: 28pt;
  }
  .hline {
    margin-top:20px;
    margin-bottom:20px;
    margin-left: 0%;
    margin-right: 0%;
    width: 1fr; 
    height: 0;   
    border-top: 2px solid gray;
  }
  .vline {
    margin-top:0%;
    margin-bottom:0%;
    margin-left: 20px;
    margin-right: 20px;
    width: 0; 
    height: 1fr;   
    border-left: 2px solid gray;
  }
  .shade {
    width: 1fr;
    background: white;
    opacity: 0.7;   
  }
  .white {
    width: 1fr;
    background: white;
  }
  .images {
    float: left;
  }
---

## 14.1. 教師無し学習
### 特徴
1. 同時密度$Pr(X)$に従う入力$X$を元に、**確率分布の特徴を推定**
2. **低次元**なら、全ての$X$から$Pr(X)$を**推定・可視化**する手法が多くある
3. 高次元では、**基本統計量**のような大まかな大域的モデルで妥協
4. **クラスタ分析**は、$X$の空間中で$Pr(X)$の**極大値**をそれぞれ含む領域を**探索可**
5. **相関ルール**は、超高次元2値データで高密度の領域を表現する記述を抽出(**連言則**)
6. 出力を直接**評価できない**

---

## 14.2. 相関ルール
商業DBをマイニングする為の人気ツールに、**相関ルール分析**がある。

+ 相関ルール分析
**頻出**の変数$X = (X_1, X_2, ..., X_p)$の**組み合わせ**を見つけるのが目的
2値データ$X_j \in  \{0,1\}$に適応

---

+ 一般的な相関ルール分析
確率密度$Pr(v_l)$が比較的高い、特徴ベクトル$X$を探すことが目的
**最頻値検出/パンプ探索**と見なせる
問題が困難
　 　↓
単純化の為に$Pr(x)$の高い$x$の代わりに$X$の空間での**大きさ**や**確率の高い領域**を探すことが目的
対応する部分集合内の値を同時にとる確率が高くなるような**部分集合**$s_1, ..., s_p$を見つける。この時、確率$Pr$の内部の形は、**連言則**という。

$$Pr \bigg[ \cap^p_{j = 1} (X_j \in s_j) \bigg] \tag{14.2}$$

---

## 14.2.1. バスケット分析
非常に大きな商業DBでは、更なる単純化が必要である。
**アイテム集合**$\mathcal K \subset \{1, ..., K\}$と各$X$の要素$v_{lj}$を元に新たな集合$Z$を使って、
$$Pr \bigg[ \cap_{k \in \mathcal K} (Z_k = 1) \bigg] = Pr\bigg[\prod_{k \in \mathcal K} Z_k = 1 \bigg] \tag{14.4}$$
14.4の推定値は、連言が真となるDBでの観測の割合から得られる
$$\hat{Pr} \bigg[ \prod_{k \in \mathcal K} Z_k = 1 \bigg] = \frac{1}{N} \sum^N_{i = 1} \prod_{k \in \mathcal K} z_{ik} \tag{14.5}$$
14.5をアイテム集合$\mathcal K$支持度・普及度$T(\mathcal K)$と呼ぶ

---
相関ルールマイニングでは、支持度の下界$t$を設定し、DB中の支持度が$t$より大きい変数集合$Z_1, ..., Z_K$で構成される全てのアイテム集合$\mathcal K$を見つける。
$$\{ \mathcal K_l | T(\mathcal K_l) > t \}\tag{14.6}$$

---

## 14.2.2. アプリオリアルゴリズム
$2^K$通りある全アイテム集合の**わずかな一部**が満たすように閾値$t$が設定されているとき、超大規模なDBでも実行可能な計算量で(14.6)の解を得られる。
上記は、次元の呪いに関する以下の性質を有効活用している。
1. 度数$|\{\mathcal K_l | T( \mathcal K_l ) > t\}|$が比較的低い
2. $\mathcal K$の部分集合で構成されるアイテム集合$\mathcal L$は、$\mathcal K$以上の支持度を持つ
 $\mathcal L \subseteq \mathcal K \Rightarrow T(\mathcal L) \geq T(\mathcal K)$

---
データ走査回数
1. **1アイテムのみ**を含むアイテム集合の**支持度を計算**
2. 前回の走査で残ったアイテムのペアから**2アイテム**のアイテム集合の支持度を計算
$\vdots$

$|\mathcal K| = m$である全ての頻出アイテムを列挙するために、1アイテムを除いて得られる大きさ$m-1$の$m$通りの前回のアイテム集合が頻出であるアイテム集合を候補にする

---
**アプリオリアルゴリズム**を使うと、各$|\mathcal K|$において1回のみデータ走査すればよい

アプリオリアルゴリズムで得られた支持度が高いアイテム集合$\mathcal K$ $\rightarrow$ 相関ルールに変換
互いに素な部分集合$A \cup B = \mathcal K$を使って、
$$A \Rightarrow B \tag{14.7}$$
この時の$A$を前提部、$B$を結論部と呼ぶ
相関ルールはDB内の前提部と結論部の**アイテム集合がどれだけ普及しているか**に基づき特徴が定義される

---
**確信度**/**信頼度**は規則の支持度を前庭部の支持度で割った値
$Pr(B|A)$の推定値
$$C(A \Rightarrow B) = \frac{T(A \Rightarrow B)}{T(A)} \tag{14.8}$$

確信度を期待確信度で割った値、**リフト値**
相関度$Pr(A and B) / Pr(A)Pr(B)$の推定値
$$L(A \Rightarrow B) = \frac{C(A \Rightarrow B)}{T(B)}$$

アプリオリアルゴリズムは、閾値$t$よりも高い支持度を持つ全アイテム集合を抽出する

---

## 14.2.4. 教師あり学習としての教師無し学習

---

## 14.2.5. 一般化相関ルール

---

## 14.2.6. 教師あり学習の選び方
- **cart決定木**
 **cart**を結合データに適応して、互いに素な領域でデータ全体に渡る目標分布のモデル化を試みる決定木を作成することができる

- cart(決定木)

---

## 14.3. クラスタ分析
クラスタ分析の目的
1. オブジェクト集合を部分集合「**クラスタ**」に**分割**
 他オブジェとの関連を表現
2. 異なる性質を持つ部分オブジェクト間の**記述統計量**の算出
 データ全体が構成されているか調べられる
3. オブジェクト間の類似度に基づいて、クラスタリングされる

---
**K平均クラスタリング**
1. クラスタ中心の初期値を与える
2. 各データ点に対して、最も近いクラスタ中心を特定
3. 各クラスタ中心を、その中心が最も近いデータ点の平均を置き換える

K平均が**トップダウン** $\leftrightarrow$ 他クラスタリング法は**ボトムアップ**
また、全クラスタリング法において、距離/**非類似度尺度**の選択が基礎である

---

## 14.3.1. 類似度行列

---

## 14.3.2. 属性に基づく非類似度

---

## 14.3.3. オブジェクト間非類似度
欠損値がある際は取り除くのが一般的

---

## 14.3.4. クラスタリングアルゴリズム
+ 組み合わせアルゴリズム ... 観測データを直接扱う
+ 混合モデル ... データが**確率密度関数に従う**母集団からの標本と仮定して考える
+ 最頻値探索器 ... ノンパラメトリックな観点で確率密度関数の各極大点を直接推定
