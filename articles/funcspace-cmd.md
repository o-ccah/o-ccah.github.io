# 関数空間のコマンドを作った

## 背景

これまでは，文書の中で関数空間を使うとき，文書ごとにプリアンブルで次のようなコマンドを定義していた．

```latex
\newcommand{\Conti}{C}
```

こうしておいて，たとえば位相空間 $ X $ 上の連続関数の空間を出力するには，`\Conti(X)` と書く．

このように関数空間の記号をコマンドにしておけば，たとえば $ C $ ではなく $ \mathscr{C} $ にしたくなったときには，上の定義を次のように直すだけで済む．

```latex
\newcommand{\Conti}{\mathscr{C}}
```

ところが，これではまだコマンド化が不十分だと思うことが多くなった．たとえば，複素数値関数を考えていることを明示したい場合には `\Conti(X; \mathbb{C})` のように書いて $ C(X; \mathbb{C}) $ と出力させるわけだが，セミコロンではなくコンマにしたくなった場合，これだとすべての出現場所で置換をしなければならない．要するに，`(X)` や `(X; \mathbb{C})` の部分まで含めてコマンド化したくなったわけである．

「$ C(X) $」も「$ C(X; \mathbb{C}) $」も僕が書く文書にはよく出てくるので，これら両方に対応したい．また，$ C $ だとあまりないが，たとえば $ L^p $ ノルムという意味で $ \lVert-\rVert_{L^p} $ と書くことはよくある．このような「単独使用」にも対応したい．

## 実装

以上を踏まえて，他のよく使う関数空間も考慮に入れ，自分用のパッケージで次のようにコマンドを定義した．

以下のコードにおいて，`\mscrM` などは同じファイル内で定義されている自分用のコマンドで，`\mathscr{M}` などの短縮形である．

また，好きな位置にオプション引数を設定できるように，xparse パッケージを使った．`\IfValueTF` コマンドは同パッケージで提供されているものである．これらについて，[このページ](https://qiita.com/zr_tex8r/items/50168ad7087516c3e139)を参考にした．

```latex
\newcommand{\BddModifier}{\mathrm{b}}%   bounded
\newcommand{\VanModifier}{0}%            vanish at infinity
\newcommand{\CptModifier}{\mathrm{c}}%   compact support
\newcommand{\LocModifier}{\mathrm{loc}}% local

\newcommand{\ClassSymbol}[2][]{C_{#1}^{#2}}%                             C^r class
\newcommand{\ClassBddSymbol}[1]{\ClassSymbol[\BddModifier]{#1}}%         C^r class, bounded
\newcommand{\ClassVanSymbol}[1]{\ClassSymbol[\VanModifier]{#1}}%         C^r class, vanish at infinity
\newcommand{\ClassCptSymbol}[1]{\ClassSymbol[\CptModifier]{#1}}%         C^r class, compact support
\newcommand{\ContiSymbol}[1][]{C_{#1}}%                                  continuous
\newcommand{\ContiBddSymbol}{\ContiSymbol[\BddModifier]}%                continuous, bounded
\newcommand{\ContiVanSymbol}{\ContiSymbol[\VanModifier]}%                continuous, vanish at infinity
\newcommand{\ContiCptSymbol}{\ContiSymbol[\CptModifier]}%                continuous, compact support
\newcommand{\SmoothSymbol}[1][]{C_{#1}^\infty}%                          smooth
\newcommand{\SmoothBddSymbol}{\SmoothSymbol[\BddModifier]}%              smooth, bounded
\newcommand{\SmoothVanSymbol}{\SmoothSymbol[\VanModifier]}%              smooth, vanish at infinity
\newcommand{\SmoothCptSymbol}{\SmoothSymbol[\mathrm{c}]}%                smooth, compact support
\newcommand{\LebesgueSymbol}[2][]{L_{#1}^{#2}}%                          Lebesgue
\newcommand{\LebesgueVanSymbol}[1]{\LebesgueSymbol[\VanModifier]{#1}}%   Lebesgue, vanish at infinity
\newcommand{\LebesgueLocSymbol}[1]{\LebesgueSymbol[\LocModifier]{#1}}%   Lebesgue, local
\newcommand{\lebesgueSymbol}[2][]{l_{#1}^{#2}}%                          Small Lebesgue
\newcommand{\SobolevSymbol}[3][]{W_{#1}^{#2, #3}}%                       Sobolev
\newcommand{\SobolevVanSymbol}[2]{\SobolevSymbol[\VanModifier]{#1}{#2}}% Sobolev, vanish at infinity
\newcommand{\SobolevLocSymbol}[2]{\SobolevSymbol[\LocModifier]{#1}{#2}}% Sobolev, local
\newcommand{\HSobolevSymbol}[2][]{H_{#1}^{#2}}%                          L^2 Sobolev
\newcommand{\HSobolevVanSymbol}[1]{\HSobolevSymbol[\VanModifier]{#1}}%   L^2 Sobolev, vanish at infinity
\newcommand{\HSobolevLocSymbol}[1]{\HSobolevSymbol[\LocModifier]{#1}}%   L^2 Sobolev, local
\newcommand{\MeasSymbol}[1][]{\mscrM_{#1}}%                              Radon measures
\newcommand{\MeasBddSymbol}[1][]{\mscrM^1_{#1}}%                         bounded Radon measures
\newcommand{\TestSymbol}[1][]{\mscrD_{#1}}%                              test functions
\newcommand{\SchwartzSymbol}[1][]{\mscrS_{#1}}%                          rapidly decreasing
\newcommand{\TestCptSymbol}[1][]{\mscrE_{#1}}%                           test functions for compact supported distributions
\newcommand{\DistSymbol}[1][]{\mscrD'_{#1}}%                             distributions
\newcommand{\TemperedSymbol}[1][]{\mscrS'_{#1}}%                         tempered distributions
\newcommand{\DistCptSymbol}[1][]{\mscrE'_{#1}}%                          compact supported distributions
\newcommand{\LinearSymbol}[1][]{\mscrL_{#1}}%                            continuous linear operators
\newcommand{\LinearCptSymbol}[1][]{\mathscr{LC}_{#1}}%                   compact linear operators

\NewDocumentCommand\FuncSpaceFormat{m m m}{#1\IfValueTF{#3}{(#2; #3)}{(#2)}}

\NewDocumentCommand\Class{O{} m m o}{\FuncSpaceFormat{\ClassSymbol[#1]{#2}}{#3}{#4}}
\NewDocumentCommand\ClassBdd{m m o}{\FuncSpaceFormat{\ClassBddSymbol{#1}}{#2}{#3}}
\NewDocumentCommand\ClassVan{m m o}{\FuncSpaceFormat{\ClassVanSymbol{#1}}{#2}{#3}}
\NewDocumentCommand\ClassCpt{m m o}{\FuncSpaceFormat{\ClassCptSymbol{#1}}{#2}{#3}}
\NewDocumentCommand\Conti{O{} m o}{\FuncSpaceFormat{\ContiSymbol[#1]}{#2}{#3}}
\NewDocumentCommand\ContiBdd{m o}{\FuncSpaceFormat{\ContiBddSymbol}{#1}{#2}}
\NewDocumentCommand\ContiVan{m o}{\FuncSpaceFormat{\ContiVanSymbol}{#1}{#2}}
\NewDocumentCommand\ContiCpt{m o}{\FuncSpaceFormat{\ContiCptSymbol}{#1}{#2}}
\NewDocumentCommand\Smooth{O{} m o}{\FuncSpaceFormat{\SmoothSymbol[#1]}{#2}{#3}}
\NewDocumentCommand\SmoothBdd{m o}{\FuncSpaceFormat{\SmoothBddSymbol}{#1}{#2}}
\NewDocumentCommand\SmoothVan{m o}{\FuncSpaceFormat{\SmoothVanSymbol}{#1}{#2}}
\NewDocumentCommand\SmoothCpt{m o}{\FuncSpaceFormat{\SmoothCptSymbol}{#1}{#2}}
\NewDocumentCommand\Lebesgue{O{} m m o}{\FuncSpaceFormat{\LebesgueSymbol[#1]{#2}}{#3}{#4}}
\NewDocumentCommand\LebesgueVan{m m o}{\FuncSpaceFormat{\LebesgueVanSymbol{#1}}{#2}{#3}}
\NewDocumentCommand\LebesgueLoc{m m o}{\FuncSpaceFormat{\LebesgueLocSymbol{#1}}{#2}{#3}}
\NewDocumentCommand\lebesgue{O{} m m o}{\FuncSpaceFormat{\lebesgueSymbol[#1]{#2}}{#3}{#4}}
\NewDocumentCommand\Sobolev{O{} m m m o}{\FuncSpaceFormat{\SobolevSymbol[#1]{#2}{#3}}{#4}{#5}}
\NewDocumentCommand\SobolevVan{m m m o}{\FuncSpaceFormat{\SobolevVanSymbol{#1}{#2}}{#3}{#4}}
\NewDocumentCommand\SobolevLoc{m m m o}{\FuncSpaceFormat{\SobolevLocSymbol{#1}{#2}}{#3}{#4}}
\NewDocumentCommand\HSobolev{O{} m m o}{\FuncSpaceFormat{\HSobolevSymbol[#1]{#2}}{#3}{#4}}
\NewDocumentCommand\HSobolevVan{m m o}{\FuncSpaceFormat{\HSobolevVanSymbol{#1}}{#2}{#3}}
\NewDocumentCommand\HSobolevLoc{m m o}{\FuncSpaceFormat{\HSobolevLocSymbol{#1}}{#2}{#3}}
\NewDocumentCommand\Meas{O{} m o}{\FuncSpaceFormat{\MeasSymbol[#1]}{#2}{#3}}
\NewDocumentCommand\MeasBdd{O{} m o}{\FuncSpaceFormat{\MeasBddSymbol[#1]}{#2}{#3}}
\NewDocumentCommand\Test{O{} m o}{\FuncSpaceFormat{\TestSymbol[#1]}{#2}{#3}}
\NewDocumentCommand\Schwartz{O{} m o}{\FuncSpaceFormat{\SchwartzSymbol[#1]}{#2}{#3}}
\NewDocumentCommand\TestCpt{O{} m o}{\FuncSpaceFormat{\TestCptSymbol[#1]}{#2}{#3}}
\NewDocumentCommand\Dist{O{} m o}{\FuncSpaceFormat{\DistSymbol[#1]}{#2}{#3}}
\NewDocumentCommand\Tempered{O{} m o}{\FuncSpaceFormat{\TemperedSymbol[#1]}{#2}{#3}}
\NewDocumentCommand\DistCpt{O{} m o}{\FuncSpaceFormat{\DistCptSymbol[#1]}{#2}{#3}}
\NewDocumentCommand\Linear{O{} m o}{\FuncSpaceFormat{\LinearSymbol[#1]}{#2}{#3}}
\NewDocumentCommand\LinearCpt{O{} m o}{\FuncSpaceFormat{\LinearCptSymbol[#1]}{#2}{#3}}
```

## 例

* `\ContiSymbol` → $ C $
* `\Conti{X}` → $ C(X) $
* `\Conti{X}[\mathbb{C}]` → $ C(X; \mathbb{C}) $
