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

## 14.3.6. K平均クラスタリング
**K平均法 (k-means)** とは、最もよく利用される繰り返し降下クラスタリング法の1つ。

1. ランダムにクラスタの中心を選択(初期化)
2. 変数をユークリッド距離で最も近いクラスタに割り当て
3. 各クラスタの変数からクラスタの中心を再選択
4. クラスタの中心が変わらなくなるまで2~3を繰り返す

---
### K平均法の例


---
### K平均法の公式
非類似度として、**2乗ユークリッド距離**が使われる。
$$d(x_i, x_{i'}) = \| x_i -x_{i'} \| ^2$$

観測$i$をクラスタ$k$に割り当てるために**符号化器**$C(i)$が使われる。
**クラスタ内分散**は、平均ベクトル$\bar x_k$と$N_k = \sum^N_{i=1}I(C(i) = k)$より、
$$W(C) = \sum^K_{k = 1} N_k \sum_{C(i) = k} \| x_i - \bar x_k \|^2$$

---
観測のあらゆる集合$S$で(14.32)が成り立つため、
$$\bar x_S = \underset{m}{argmin} \sum_{i \in S}\|x_i - m\|^2$$

目的を達成する符号化器を求める**繰り返し降下アルゴリズム**が、
$$C^* = \underset{C}{min} \sum^K_{k=1} N_k \sum_{C(i)=k} \| x_i - \bar x_k \|^2 $$

$C^*$を算出する際には、以下の**最適化問題**を扱う。
$$\underset{C, \{ m_k \}^K_1 }{min} \sum^K_{k = 1} M_k \sum_{C(i)=k} \| x_i - \bar m_k \|^2 $$

---
### K平均法のメリット
1. 計算が容易
2. **大規模なデータセット**でも利用可能

### K平均法のデメリット
1. **球状**以外のクラスタは正しく捉えにくい
2. クラスタ数$k$を決める必要
3. **外れ値**の影響を受けやすい
4. 初期クラスタ中心により**結果が変動**
 $\rightarrow$ 準最適な極所解

---

## 14.3.7. 混合ガウス
K平均法と**混合ガウス分布**を推定するための**EMアルゴリズム**が関連している。

+ 混合ガウス分布(GMM) ... 複数の正規分布(ガウス分布)の組み合わせで、データ全体の確率分散を表現する統計モデル
+ EMアルゴリズム ... 確率モデルのパラメータを**最尤推定**する手法の1つ

---
EMアルゴリズムは、**Eステップ**と**Mステップ**の繰り返しであり、
1. Eステップで観測不可能な潜在変数の**事後確率**を求める (= モデルの尤度の期待値)
2. Mステップで観測不可能な潜在変数の事後確率を最大化する**パラメータ**を求める

これが、k平均法のクラスタへの割り当て~クラスタの中心の再選択に似ている。

---

## 14.3.9. ベクトル量子化
**ベクトル量子化(VQ)** とは、ベクトル内の一部をブロックに分割する手法である。
分割したブロック内で**コードワード**(最も近い中心)で近似し、1つの値にする。
復号には、中心の集合である**コードブック**を利用する。

使い道としては、
1. データ圧縮
2. **次元圧縮**
3. 特徴量エンジニアリング

---
### ベクトル量子化の例


---

## 14.3.10. Kメドイドクラスタリング
**Kメドイド法**とは、K平均法同様に非階層的なクラスタリングアルゴリズムである。

1. **任意の非類似度**$D$で、クラスタの**中心とするデータ点**を選択
 クラスタ中心集合$i^*_k = \underset{\{ i:C(i)=k \}}{argmin} \sum_{C(i')=k} D(x_i, x_{i'})$
2. 各クラスタの中心のデータ点から、各変数をクラスタに再割り当て
 クラスタ割り当て$C(i) = \underset{ i \leq k \leq K}{argmin} D(x_i, m_k)$
3. 割り当ての変更がなくなるまで、1~2を繰り返す

---
### Kメドイド法の例


---
### Kメドイド法のメリット
1. **外れ値**の影響を受けにくい
2. **任意の非類似度**が使える (マンハッタン距離(L1)、ユークリッド距離(L2)等)
3. 解釈性

### Kメドイド法のデメリット
1. **計算量の多さ** (Kメドイド法 >> K平均法)
2. 初期クラスタ中心により**結果が変動**

---

## 14.3.11. 実用上の問題
K平均法・Kメドイド法は**クラスタ数**$K^*$や**初期値**を決める必要がある。
初期値は、以下のどちらかがあれば良い。
1. 中心$\{ m_1 , ..., m_K \}$や$\{ i_1, ..., i_K \}$の**初期集合**
2. **初期符号器**$C(i)$

通常は中心の初期集合の方が便利

---
初期化の手法としては、単純な**乱数**~**前浮き漸次的割り当て**まで多岐にわたる。

クラスタ数$K^*$の選択は、**目的に依存する**。
特に、クラスタ分析により**自然なグループに分離できているか**を確かめる際には、
データから**クラスタ数を推定**する必要がある。
この推定は、**経験則**や**直感**に基づく準最適解を導く手法が多い。

---

## 14.3.12. 階層的クラスタリング
階層的クラスタリングは、K平均法やKメドイド法と比べて以下の1つの特徴がある。
1. **初期値**が存在しない
2. 階層的なクラスタが作成可能である
 2.1. 最も下の階層では、各クラスタは**1つの観測**のみ
 2.2. 最も上の階層では、**全観測を含む1つのクラスタ**のみ
3. **凝集型(ボトムアップ)** と**分割型(トップダウン)** の2種類がある
4. 再帰的な2つずつの分割や凝縮は**根付き二分木**で表現可 (**デンドログラム**)

---
### 階層的クラスタリングの例


---
デンドログラムは**視覚的な要約**として有用で、以下のような特徴がある。
1. 上位の階層で統合されたクラスタは**自然なクラスタ**の候補
2. **階層的手法**や**わずかなデータの相違**により、異なるデンドログラムが得られる

---
デンドログラムにより生成された階層構造が、どれだけデータを表現できているか、**共表形相関係数**で判断できる。

これは、
+ $N(N-1)/2$個の**観測間非類似度**$d_{ii'}$
+ **共表形非類似度**$C_{ii'} \leq max(C_{ik}, C_{i'k})$ 　 (任意の3つの観測点$i, i', k$)

の相関係数である。

---
### 凝縮型クラスタリング
個々のデータ点を**クラスタと見なし**、クラスタが1つになるまで結合させていく方式
使用頻度が**高い**
1. 全てのクラスタで**対称行列**を作る
2. **最も距離が大きいクラスタ**を最小にするようにクラスタを結合
3. 対称行列を作り直す
4. クラスタが1つになるまで、2~3を繰り返す

---
凝縮型クラスタリングでは、**クラスタ間の距離の違い**で以下の3つが良く使われる。
1. **単連結** ... グループの非類似度に**最短距離法**を使う
$$d_{SL} (G, H) = \underset{i'\in H}{\underset{i \in G}{min}} d_{ii'}$$
2. **完全連結** ... グループの非類似度に**最長距離法**を使う
$$d_{CL} (G, H) = \underset{i'\in H}{\underset{i \in G}{max}} d_{ii'}$$
3. **群平均** ... **グループ間**の平均類似度を使う。
$$d_{GA} (G, H) = \frac{1}{N_G N_H} \sum_{i \in G} \sum_{i' \in H} d_{ii'}$$

---
前述の凝縮型クラスタリングの違いは以下の通り


---
### 分割型クラスタリング
**全データのクラスタ**からデータ点が1つだけ含まれるクラスタまで分割を繰り返す方式
使用頻度が低い
**k平均法**や**kメドイド法**もこの分割型クラスタリングに含まれる

---

## 14.4. 自己組織化マップ
**自己組織化マップ(SOM)** は、K平均法の**制約付き版**と見なせ、以下の特徴がある。
1. 高次元データを2次元座標系に写像できる (**制約付き位相マップ**)
 $\rightarrow$ 視覚的な理解が可
2. 入力の近さをマップ上での近さで表現
 $\rightarrow$ **データ間の関係が失われない**

---
自己組織化マップの手順は以下の通り
1. 2次元格子上の$K$個の**プロトタイプ$m_j$を初期化**
2. 入力$x_i$を1つ取り出し、**最も近い**プロトタイプ$m_j$を探す
3. 全てのプロトタイプ$m_k$を$x_i$の方へ近づける
$$m_k \leftarrow m_k + \alpha (x_i - m_k) \tag{14.46}$$
4. 2~3を全ての入力において行う

---
### 自己組織化マップの例

---
### 自己組織化マップのメリット
1. 次元圧縮
2. データの**構造**や**類似性**の保持

### 自己組織化マップのデメリット
1. 明確なクラスタの**ラベル**が存在しない
2. **初期値**やデータの**順番**に依存
 $\rightarrow$ 実用上では、前述の手順を**複数回**行い、一巡毎にデータをシャッフルする

---
自己組織化マップの変数には、**学習率**$\alpha$と**距離閾値**$r$がある。
+ 学習率$\alpha$は**数千ステップ**かけて$1.0 \rightarrow 0.0$の様に減少させる。 
+ 距離閾値$r$も**数千ステップ**かけて$R \rightarrow 1$の様に減少させる。

---
洗練された自己組織化マップでは、**距離によって**プロトタイプの更新則を変更する。
**近傍関数**$h$、座標$l_i$を使って、
$$m_k \leftarrow m_k + \alpha h (\| l_j - l_k \|)(x_i - m_k) \tag{14.47}$$

また、バッチ版では**重み**$w_k$を使って、
$$m_j = \frac{\sum w_k x_k}{\sum w_k}$$

---

## 参考文献
[1] 【目で見てわかる】k-meansクラスタリングの基本から限界まで #Python - Qiita (参照:2025/06/20)
https://qiita.com/ryo18/items/4a775aeec61de07d2548

[2] ベクトル量子化 - 環境と品質のためのデータサイエンス (参照:2025/06/22)
https://data-science.tokyo/ed/edj1-5-3-5-2.html

[3] k-medoids法 | 今更聞けないIT用語集 | 株式会社APPSWINGBY (参照:2025/06/22)
https://appswingby.com/k-medoids%E6%B3%95-%E4%BB%8A%E6%9B%B4%E8%81%9E%E3%81%91%E3%81%AA%E3%81%84it%E7%94%A8%E8%AA%9E%E9%9B%86/

---

[4] 機械学習：階層的クラスタリング　凝縮型階層的アルゴリズム｜Dean4rmEdinburgh  (参照:2025/06/23)
https://note.com/dean_ediburgh/n/n402bfd92d380

[5] 5分で分かる自己組織化マップ | PPT (参照:2025/06/23)
https://www.slideshare.net/slideshow/5-13781247/13781247#84

[6] 自己組織化マップ(Self-Organizing Map, SOM)～非線形の可視化・見える化手法、ただ過学習の危険性も高いので注意！～ | データ化学工学研究室(金子研究室)＠明治大学 理工学部 応用化学科 (参照:2025/06/23)
https://datachemeng.com/selforganizingmap/