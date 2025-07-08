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
    color: #0B3E8D;
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

## 14.6.1. アーキタイプ分析(Archetypal analysis)
観測データをそのデータの**アーキタイプ(多次元データ内の極値)** の混合によって近似する計算手法 [1]
 $\rightarrow$ Kmeansに似ている

+ 特徴抽出や次元削減に利用(データの外側の点を調べることで、**概形がわかる**)
 $\rightarrow$ 直感的に理解しやすい表現へ
+ AAはデータの線形変換やスケーリングに対して不変 [2]

---
### 14.7.1 潜在変数と因子分析
特異値分解(SVD)$X = UDV^T$は**潜在変数**で表せる。
+ $S = \sqrt N U, A^T = DV^T / \sqrt N$

導入した2つの変数を使い、$X = SA^T$と表せる。

$U$が直交しており、$X$の列(= $U$の列)の平均が$0$と仮定すると、
1. $S$の列の平均は$0$、分散は1で無相関
 $\rightarrow$ SVDやPCAは**潜在変数モデルの推定値と見なせる**
2. **因子分析**とは、**$X_p$の相関構造をモデル化すること**
 $\rightarrow$ 原因究明や仮設の検証に使われる [3]

$$X_p = a_{p1} S_1 + a_{p2} S_2 + ... + a_{pp} S_p \tag{14.78}$$

識別性の問題は残っており、現代の統計では因子分解はあまり使われていない

---
### 14.7.2 独立成分分析(ICA)
ICAとは、複数の観測データ/信号から独立な成分を推定する技術である [4]
可能な限り**正規分布から遠ざかる**ような直交射影の列を探す
 $\rightarrow$ 白色化データにおいては、**独立な成分を探すこと**
そして、独立な成分につながる**回転**を探す

ICAでは、(14.78)とほぼ同じものを考えるが$S_p$が**無相関ではなく統計的に独立である**という仮定をおく。これにより、因子分解の**識別性の問題が解決できる**。 [5]

実用上では、**話者分離**などに活用される [6]

---
### 14.7.3 探索的射影追求
高次元$\rightarrow$低次元の射影は**ほぼ正規分布**に従う。
よって、クラスタ等の構造は**非正規分布の射影に依存する**という考え。

$$Y_j = a_j^T X$$

---
### 14.8 多次元尺度構成法(MDS)
MDSは**入力変数の各要素毎の距離**を計算し、高次元から**低次元にマッピング**する手法
+ MDSでは**距離(類似度)**$d_{ij}$が必要
+ 自己組織化マップ(SOM)や主曲線・主曲面は**データ**$x_i$が必要

MDSでは、全ての要素毎の距離を明示的に保持しようとする
+ SOMや主平面で起きていた、特徴空間では**離れた点も近接してマッピング**される現象を回避することができる

---

## 参考

[1] https://en.wikipedia.org/wiki/Archetypal_analysis

[2] https://www.themoonlight.io/ja/review/a-survey-on-archetypal-analysis

[3] https://data-science.tokyo/ed/edj1-2-4.html

[4] https://ja.wikipedia.org/wiki/%E7%8B%AC%E7%AB%8B%E6%88%90%E5%88%86%E5%88%86%E6%9E%90

[5] https://qiita.com/Miyabi1456/items/3fdc5a1603269db197d5

[6] https://data-science.tokyo/ed/edj1-2-4-2.html