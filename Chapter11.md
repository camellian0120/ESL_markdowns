---
marp: false
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
## 11.2. 射影追跡回帰
射影追跡回帰(projection pursuit regression, PPR)は回帰モデルの一種で、以下の式で表される。\
ただし、入力$X$は縦ベクトル、$\omega_m$は縦ベクトル、$M$は**非線形の関数の数**である。\
また、関数$g_m$は**事前に形状は定められておらず**、平滑化手法によって推定される。
$$f(X) = \sum^M_{m = 1} g_m (\omega^T_m X) \tag{11.1}$$

+ 特徴
 - 説明変数に**平滑化関数を適用する前に**、最適な方向における**行列を最初に予測する**ことで加法モデルを拡張
 - **リッジ関数**$g_m (\omega^T_m X)$は**非線形関数**で、うまく取れば$M$が大きくても任意の精度で近似可能

---
例外として、非線形の関数の個数$M = 1$の場合は、**単一指標モデル**と呼ばれる。\
このモデルは、線型回帰を**わずかに一般化した**ものと考えられ、以下の式で表せる。
$$f(X) = g_1 (\omega^T_1 X)$$

---
訓練データ$(x_i, y_i) 　 (i = 1, 2, ..., N)$に対して当てはめを行うには、式(11.2)の誤差関数を利用する。\
リッジ関数$g_m$及び重み$\omega_m$を**近似的に最小化**すれば良い。\
ただし、過学習を避けるために$g_m$の**複雑度に関する制約は必須**である。

$$\sum^N_{i=1} \bigg[ y_i - \sum^M_{m = 1} g_m (\omega^T_m x_i) \bigg]^2 \tag{11.2}$$

---
射影追跡回帰の手順は以下のとおりである。
1. 標本の準備
 入力データを**中心化**/**球状化** (まとめて**白色化**と言う)
2. 重み$\omega$が収束するまで更新する

---
### 射影追跡回帰のメリット
1. 予測に有用

### 射影追跡回帰のデメリット
1. 解釈性に乏しい

---

## 11.3. ニューラルネットワーク(NN)

---

## 11.4. NNの当てはめ

---

## 11.5. NNの訓練時の問題点

---

## 11.5.1. 初期値

---

## 11.5.2. 過学習

---

## 11.5.3. 入力のスケーリング

---

## 11.5.4. 隠れユニット/隠れ層の数

---

## 11.5.5. 複数の極小解

---

## 11.8. 考察

---

## 11.9. ベイズNN, NIPS2003チャレンジ

---

## 11.9.1. ベイズ, ブースティング, バギング

---

## 11.9.2. 性能比較

---

## 11.10. 計算上考慮すべき事柄


---
## 参考文献

[1] 射影追跡回帰 - Wikipedia (参照 : 2025/07/03)
https://ja.wikipedia.org/wiki/%E5%B0%84%E5%BD%B1%E8%BF%BD%E8%B7%A1%E5%9B%9E%E5%B8%B0

[2] 

