---
marp: true
math: mathjax
header: "ESL輪読"
paginate: true
style: |
  strong {
    color: #C9B124;
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
---

# 4.1 はじめに
分類問題における線形手法:

1. 分類問題では、入力空間を**異なるクラスに分割**する決定境界が重要
1. 線形決定境界は、異なる方法で構築可能
1. 最も簡単な方法は、**クラスインジケータ変数**に線形回帰を適用
1. 分類は、最大の**判別関数値**または**事後確率**に基づいて行われる
1. 非線形決定境界を得るには、入力変数の**基底変換（二乗項や交互作用項の追加）** が有効

---

---

# 4.2 インジケータ行列の線形回帰
**クラスインジケータ変数**を用いた線形回帰による分類手法:

1. 各クラスに対してインジケータ変数を作成
1. 線形回帰モデルを各インジケータ変数に適用
1. 新しい観測値は、**最大の推定値を持つクラス**に分類
1. K ≥ 3の場合、「**マスキング**」の問題が発生する可能性がある
1. 多クラス問題では、この手法は信頼性が低い

---

---

# 4.3 線形判別分析 (LDA)
線形判別分析:

1. ガウス分布を仮定した分類手法
1. クラス間で共通の分散共分散行列を仮定
1. 決定境界は線形
1. パラメータは訓練データから推定
1. 次元削減と分類に有効
1. **正則化判別分析（RDA）** により、モデルの柔軟性を向上
1. 特に4.3.3の「**次元削減線形判別分析**」では、**centroid（クラス重心）** を用いた最適な低次元部分空間の発見方法を詳しく説明しています。

---

