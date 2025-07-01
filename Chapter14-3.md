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

## 14.5.1.主成分分析
イメージとしては、**「与えられた特徴量から新たな特徴量（主成分）を作り出し、元の特徴量よりも少ない数の変数（次元）でデータを説明する」**

+ 次元削減（可視化）の最も基本的な手法
+ 多変量データをより少数のパラメータ情報に圧縮
+ 2次元に圧縮することで、多次元データを可視化することが可能
+ 座標系の回転変換（アフィン変換）を行い、より少ない座標軸でデータを説明
+ 投射後のデータの散らばりが最大になるように、データをより低次元の空間に投影
+ 教師なし学習の一種 [1]

---

## 14.5.2. 主成分と主曲線
主成分線を一般化し、近似した滑らかな1次元曲線近似を**主曲線**と言う。 [2]

---

## 14.5.3. スペクトラルクラスタリング
超球状以外のクラスタ分析に使われる手法。
クラス形成を**グラフカット方式**によって実現する方法。

---

## 14.5.4. カーネル主成分分析
カーネル主成分分析は、**データを高次元に射影して**PCAをかける手法である。
$\rightarrow$ 非線形の関数データを扱える。 [3]

---

## 14.3.5. スパース主成分分析
**スパースモデリング**を取り入れたPCA。
計算結果をシンプルにするのが目標。

+ スパースモデリング ... 変数選択の1つで、**重要な変数だけ選び出す方法**。
 　 　 　 　 　 　 　 　多変数の際に有効[4]

---

## 14.6. 非負値行列因子分解(NMF)
NMFは、**非負値のデータを要素にもつ行列**を、**頻出パターン行列**とその**係数行列**に分解する手法。[5]

$\rightarrow$ 解釈性の面で、**基底ベクトルおよび係数が非負**の方が嬉しい。
　 $\rightarrow$ **係数が疎**になってわかりやすい。(図は"[6]#なんで非負なの") [6]

---

## 参考

[1] https://qiita.com/oki_kosuke/items/70c7e0bcd7b534589f69

[2] https://www.slideshare.net/slideshow/ss-51761860/51761860

[3] https://qiita.com/NoriakiOshita/items/138c10eada03938fcd79

[4] https://data-science.tokyo/ed/edj1-2-3-2-3.html

[5] https://academ-aid.com/ml/nmf

[6] https://qiita.com/nozma/items/d8dafe4e938c43fb7ad1
