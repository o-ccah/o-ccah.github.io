# 京大「解析学演義 I」の問題

Twitter で見かけた京大「解析学演義 I」の問題をやってみたので，メモしておきます．

問題は[このページ](https://www.math.kyoto-u.ac.jp/~y.arano/engi.html)にあります．解いたのは，「その 1」の問題 1, 2 です．

## 問題 1

一般性を失わず，$ 0 \leq b_n \leq 1 $ と仮定する．

$ I_0 = [0, 1] $ と置く．$ \sum_{n \in \mathbb{N}} a_n = \infty $ だから，$ I_1 = [0, 1/2] $, $ [1/2, 1] $ のどちらか少なくとも一方に対して $ \sum_{n \in \mathbb{N}, b_n \in I_1} a_n = \infty $ となる．これが成り立つように $ I_1 $ を定める．同様に，$ I_1 $ を半分ずつに分けた長さ $ 1/4 $ の区間のどちらかを適切に選んで $ I_2 $ とすれば，$ \sum_{n \in \mathbb{N}, b_n \in I_2} a_n = \infty $ となる．以下同様に繰り返して，各 $ k \in \mathbb{N} $ に対して長さ $ 2^{-k} $ の区間 $ I_k $ を減少列になるようにとり，任意の $ k \in \mathbb{N} $ に対して $ \sum_{n \in \mathbb{N}, b_n \in I_k} a_n = \infty $ となるようにできる．

$ k \in \mathbb{N} $ に関して再帰的に有限部分集合 $ S_k \subseteq \\{n \in \mathbb{N} \mid b_n \in I_k\\} $ をとり，任意の $ k $ に対して $ \sum_{n \in S_k} a_n \geq 1 $ かつ $ \max S_k < \min S_{k + 1} $ となるようにできる．$ S_0 $, $ S_1 $, $ \dots $ の元を列挙して昇順に並べたものを $ k_0 $, $ k_1 $, $ \dots $ とすれば，これが条件を満たす．

## 問題 2

一般性を失わず，$ 0 \leq a_n \leq 1 $ と仮定する．

(1) ⇒ (2): (1)が成り立つとすると，各整数 $ k \geq 1 $ に対して $ n_k \geq 1 $ を選んで，任意の $ n \geq n_k $ に対して $ \frac{1}{n} \sum_{i = 0}^{n - 1} a_i \leq 1/k^2 $ となるようにできる．$ (n_k)_{k \geq 1} $ は狭義単調増加であるとしてよい．このとき，任意の $ n \geq n_k $ に対して，$ a_0 $, $ \dots $, $ a_{n - 1} $ のうち $ 1/k $ より大きいものの割合は $ 1/k $ 以下である．

各 $ k \geq 1 $ に対して，$ I_k = \\{i \in \\{n_k, \dots, n_{k + 1} - 1\\} \mid a_i > 1/k\\} $ と置き，$ I = \bigcup_{k = 1}^{\infty} I_k $ と定めれば，これが(2)の条件を満たす．

(2) ⇒ (1): (2)が成り立つとする．$ I_n = I \cap \\{0, \dots, n - 1\\} $ と置く．

$ \epsilon > 0 $ を任意にとる．$ I $ に関する仮定より，$ n $ が十分大きければ $ \\#I_n/n \leq \epsilon $ である．また，$ \lim_{i \notin I} a_i \to 0 $ と Cesàro 平均に関するよく知られた事実より，$ n $ が十分大きければ $ (\sum_{i \in \\{0, \dots, n - 1\\} \setminus I_n} a_i)/(n - \\#I_n) \leq \epsilon $である．よって，$ n $ が十分大きければ，
\begin{align}
  \frac{1}{n} \sum_{i = 0}^{n - 1} a_i
  &= \frac{1}{n} \sum_{i \in \\{0, \dots, n - 1\\} \setminus I_n} a_i
    + \frac{1}{n} \sum_{i \in I_n} a_i \\
  &\leq \frac{1}{n - \\#I_n} \sum_{i \in \\{0, \dots, n - 1\\} \setminus I_n} a_i
    + \frac{\\#I_n}{n} \\
  &\leq \epsilon
\end{align}
である．よって，(1)が成り立つ．
