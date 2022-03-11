# 直線を直線に移す写像

[Twitter](https://twitter.com/19_97_31_23/status/1428908091270066181) で面白そうな問題を見かけました．解けたと思うのでメモしておきます．

## もとの問題

<div>
<p>以下，「直線」とは，$ \{(x, y) \in \mathbb{R}^2 \mid ax + by = c\} $（$ a $, $ b $, $ c \in \mathbb{R} $，$ (a, b) \neq (0, 0) $）という形の $ \mathbb{R}^2 $ の部分集合のことをいいます．</p>

<p><strong>問題</strong>: 写像 $ F\colon \mathbb{R}^2 \to \mathbb{R}^2 $ であって直線の像が直線になるものは，アフィン写像以外に存在するか？</p>

<p><strong>解答</strong>: 存在する．たとえば $ F(x, y) = (x + y^3, 0) $．</p>
</div>

## 修正した問題

<div>
<p>もとの問題には反例がありましたが，その反例では $ F $ の像は 1 本の直線に含まれていました．このような $ F $ を除外した問題を考えます．</p>

<p><strong>問題</strong>: 写像 $ F\colon \mathbb{R}^2 \to \mathbb{R}^2 $ であって直線の像が直線になるものは，像が 1 本の直線に含まれるものを除くと，アフィン写像以外に存在するか？</p>

<p><strong>解答</strong>: 存在しない．以下，それを証明する．$ F $ を条件を満たす写像とする．</p>

<p><strong>主張 1</strong>: $ F $ は全射である．</p>

<p><strong>証明</strong>: 直線の像が直線になるという条件より，異なる 2 点 $ p $, $ q $ が $ F $ の像に属するならば，$ p $ と $ q $ を通る直線は $ F $ の像に含まれる．また，仮定より，$ F $ の像は同一直線上にない 3 点を含む．これらより，$ F $ の像は $ \mathbb{R}^2 $ 全体である．//</p>

<p><strong>主張 2</strong>: $ \alpha $, $ \beta $ が平行でない 2 直線ならば，それらの像 $ F(\alpha) $, $ F(\beta) $ も平行でない 2 直線である．</p>

<p><strong>証明</strong>: $ \alpha \cap \beta \neq \emptyset $ より $ F(\alpha) \cap F(\beta) \neq \emptyset $ である．あとは，$ F(\alpha) \neq F(\beta) $ を示せばよい．$ F(\alpha) = F(\beta) $ と仮定する．$ F $ は全射だから（主張 1），点 $ p \in \mathbb{R}^2 $ であって $ F(p) \notin F(\alpha) = F(\beta) $ を満たすものがとれる．$ \alpha $ と $ \beta $ は平行でないから，$ p $ を通る任意の直線 $ \gamma $ は $ \alpha $ または $ \beta $ と点を共有し，したがって $ F(\gamma) $ は $ F(\alpha) = F(\beta) $ と点を共有する．したがって，$ F(\gamma) $ が「$ F(p) $ を通り $ F(\alpha) = F(\beta) $ に平行な直線」になることはない．ところが，これは $ F $ の全射性（主張 1）に反する．よって，背理法より，$ F(\alpha) \neq F(\beta) $ である．//</p>

<p><strong>主張 3</strong>: $ F $ は単射である．</p>

<p><strong>証明</strong>: 異なる 2 点 $ p $, $ q \in \mathbb{R}^2 $ について $ F(p) = F(q) $ と仮定する．$ \alpha $, $ \beta $ は異なる平行な 2 直線であって，それぞれ $ p $, $ q $ を通るとする．直線 $ F(\alpha) $ と $ F(\beta) $ は点 $ F(p) = F(q) $ を共有する．点 $ r \in \beta $ を $ F(r) \neq F(p) = F(q) $ となるようにとると，$ p $ と $ r $ を通る直線 $ \gamma $ の $ F $ による像は $ F(p) = F(q) $ と $ F(r) $ を通る直線，すなわち $ F(\beta) $ だが，これは主張 2 に反する．よって，背理法より $ F $ は単射である．//</p>

<p>以上より，$ F $ は平行でない 2 直線を平行でない 2 直線に移し，また，直線 $ \alpha $ を固定すると，$ F $ は「$ \alpha $ に平行な直線の全体」から「$ F(\alpha) $ に平行な直線の全体」への全単射を与える．</p>

<p>定義域および終域の $ \mathbb{R}^2 $ にアフィン変換を施すことで，一般性を失わず $ F(0, 0) = (0, 0) $，$ F(1, 0) = (1, 0) $，$ F(0, 1) = (0, 1) $ と仮定する．このとき，$ F $ は直線 $ x = s $ を直線 $ x = f(s) $ に移し，直線 $ y = t $ を直線 $ y = g(t) $ に移すとして全単射 $ f $, $ g\colon \mathbb{R} \to \mathbb{R} $ を定めることができる．$ F $ はこの $ f $, $ g $ を用いて
\[
  F(x, y) = (f(x), g(y))
\]
と書ける．$ F(0, 0) = (0, 0) $，$ F(1, 0) = (1, 0) $，$ F(0, 1) = (0, 1) $ より，$ f(0) = g(0) = 0 $，$ f(1) = g(1) = 1 $ である．</p>

<p>$ F(0, 0) = (0, 0) $ かつ $ F(1, 1) = (1, 1) $ だから，$ F $ は直線 $ y = x $ を直線 $ y = x $ に移す．したがって，$ f = g $ である．</p>

<p>$ F(1, 0) = (1, 0) $ かつ $ F(0, 1) = (0, 1) $ だから，$ F $ は直線 $ y = 1 - x $ を直線 $ y = 1 - x $ に移す．したがって，任意の $ x \in \mathbb{R} $ に対して $ f(1 - x) = 1 - f(x) $ である．</p>

<p>任意の $ a \in \mathbb{R} $ に対して，$ F(0, 0) = (0, 0) $ かつ $ F(1, a) = (1, f(a)) $ だから，$ F $ は直線 $ y = ax $ を直線 $ y = f(a) x $ に移す．したがって，任意の $ x \in \mathbb{R} $ に対して $ f(ax) = f(a)f(x) $ である．記号を置き直せば，任意の $ x $, $ y \in \mathbb{R} $ に対して $ f(xy) = f(x)f(y) $ となる．</p>

<p>以上より，最終的な主張は次の主張から従う．</p>

<p><strong>主張 4</strong>: 関数 $ f\colon \mathbb{R} \to \mathbb{R} $ であって，任意の $ x $, $ y \in \mathbb{R} $ に対して $ f(1 - x) = 1 - f(x) $ かつ $ f(xy) = f(x) f(y) $ を満たすものは，恒等写像のみである．</p>

<p><strong>証明</strong>: 任意の $ x $, $ y \in \mathbb{R} $ に対して，
\[
  f(x - xy)
  = f(x(1 - y))
  = f(x)f(1 - y)
  = f(x)(1 - f(y))
  = f(x) - f(x)f(y)
  = f(x) - f(xy)
\]
である．記号を置き直せば，任意の$ x $, $ y \in \mathbb{R} $，$ x + y \neq 0 $ に対して $ f(x + y) = f(x) + f(y) $ となる．この式から $ f(0) = 0 $ がわかり，したがって $ f(1) = f(1 - 0) = 1 - f(0) = 1 $ である．また，任意の $ x \in \mathbb{R} \setminus \{-1\} $ に対して
\[
  f(-x)
  = f(1 - (1 + x))
  = 1 - f(1 + x)
  = 1 - f(1) - f(x)
  = -f(x)
\]
だから，結局任意の $ x $, $ y \in \mathbb{R} $ に対して $ f(x + y) = f(x) + f(y) $ が成り立つ．以上より，$ f $ は $ \mathbb{R} $ の自己環準同型である．よく知られているように，これは恒等写像しかありえない．//</p>
</div>

## 考えられる一般化

<div>
<p>素直な一般化として，$ \mathbb{R}^2 $ を $ \mathbb{R}^n $ にしたり，「直線」をより高次元の部分アフィン空間にしたりというのがありますが，まだちゃんと考えていません．</p>
</div>