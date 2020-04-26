# 水素原子
##　はじめに
水素原子内にある電子は中心力場内の粒子のように振る舞う。これを元に水素原子内の電子の軌道を求める。以下は今回作成したプログラムや数値計算に関するドキュメントでは無い。波動関数がプログラムで使用した関数で求められることを示すものである。
### 中心力場内の粒子におけるシュレーディンガー方程式
原子の中に束縛された電子の物質波は定常波にあることから考える方程式は定常状態に対する時間に依存しないシュレーディンガー方程式であり、
$$\{-\frac{\hbar^2}{2m}\bigtriangleup+V(r)\}\varphi(\boldsymbol{r})=\epsilon\varphi(\boldsymbol{r})$$
である。ポテンシャルエネルギーを$V(r)$と記述したのは中心力場ではポテンシャルエネルギーは球対象となるからである。
この方程式には$r$以外に変数を取らないことから直角座標で扱うよりも極座標を用いたほうが計算を容易に行うことができる。極座標でのラプラシアン$\bigtriangleup$は
$$\bigtriangleup = \frac{\partial^2}{\partial{r}^2}+\frac{2}{r}\frac{\partial}{\partial r}+\frac{1}{r^2}\Lambda\\
\Lambda = \frac{1}{\sin{\theta}}\frac{\partial}{\partial\theta}(\sin\theta\frac{\partial}{\partial\theta})+\frac{1}{\sin^2\theta}\frac{\partial^2}{\partial\phi^2}$$
であるので極座標でのシュレーディンガー方程式は
$$\{-\frac{\hbar^2}{2m}(\frac{\partial^2}{\partial{r}^2}+\frac{2}{r}\frac{\partial}{\partial r}+\frac{1}{r^2}\Lambda)+V(r)\}\varphi(\boldsymbol{r})=\epsilon\varphi(\boldsymbol{r})$$
となる。波動関数をrに依存する関数$R$と$\theta,\phi$に依存する関数$Y$に以下のように分離して解く。
$$\varphi(r,\theta,\phi)=R(r)Y(\theta,\phi)$$
このときシュレーディンガー方程式は
$$
-\frac{\hbar^2}{2m}\{(\frac{\mathrm{d}^2R}{\mathrm{d}r^2}+\frac{2}{r}\frac{\mathrm{d}R}{\mathrm{d}r})Y+\frac{R}{r^2}\Lambda Y\}+V(r)RY=\epsilon RY \\
\frac{r^2}{R}(\frac{\mathrm{d}^2R}{\mathrm{d}r^2}+\frac{2}{r}\frac{\mathrm{d}R}{\mathrm{d}r})+\frac{2m}{\hbar^2}r^2(\epsilon-V(r))=-\frac{\Lambda Y}{Y}
$$
のように、左が$r$だけの関数、右が$\theta,\phi$だけの関数となるのでこれが成り立つためには両辺とも定数である必要がある。この定数を$\lambda$とし、右辺を変形すると
$$-\frac{\hbar^2}{2m}(\frac{\mathrm{d}^2R}{\mathrm{d}r^2}+\frac{2}{r}\frac{\mathrm{d}R}{\mathrm{d}r}-\frac{\lambda}{r^2}R)+V(r)R = \epsilon R$$
左辺を変形すると
$$\Lambda Y(\theta,\phi)+\lambda Y(\theta,\phi)=0$$
となる。右辺を変更したものはさらに$R(r)=\frac{1}{r}\chi(r)$と置くことによって簡単に表すことができ、
$$-\frac{\hbar^2}{2m}(\frac{d^2\chi}{dr^2}-\frac{\lambda}{r^2}\chi)+V(r)\chi=\epsilon\chi$$となる。
### 角度に関する項の計算
$\theta,\phi$に関する方程式についてまず考える。前回求めたように$\theta,\phi$の2変数による方程式は$\Lambda$を具体的な形に戻して、$$\frac{1}{\sin{\theta}}\frac{\partial}{\partial\theta}(\sin\theta\frac{\partial Y}{\partial\theta})+\frac{1}{\sin^2\theta}\frac{\partial^2Y}{\partial\phi^2}+\lambda Y = 0$$とかける。
ここでさらに$Y(\theta,\phi)$を$Y(\theta,\phi)=\Theta(\theta)\Phi(\phi)$のように$\theta$についての関数と$\phi$についての関数に変数分離させる。このとき今考えている方程式は
$$\frac{\Phi}{\sin{\theta}}\frac{\mathrm{d}}{\mathrm{d}\theta}(\sin\theta\frac{\mathrm{d}\Theta}{\mathrm{d}\theta})+\frac{\Theta}{\sin^2\theta}\frac{\mathrm{d}^2\Phi}{\mathrm{d}\phi^2}+\lambda \Theta\Phi = 0\\
\frac{\sin\theta}{\Theta}\frac{\mathrm{d}}{\mathrm{d}\theta}(\sin\theta\frac{\mathrm{d}\Theta}{\mathrm{d}\theta})+\sin^2\theta\lambda = -\frac{1}{\Phi}\frac{\mathrm{d}^2\Phi}{\mathrm{d}\phi^2}
$$
のようになる。先程同様左辺が$\theta$だけの式に、右辺が$\phi$だけの式になっているので両辺とも定数である必要があり、これを$\nu$とする。これを受けて2式に分離させると、
$$\frac{\mathrm{d}^2\Phi}{\mathrm{d}\phi^2}+\nu\Phi=0\\
\frac{1}{\sin\theta}\frac{\mathrm{d}}{\mathrm{d}\theta}(\sin\theta\frac{\mathrm{d}\Theta}{\mathrm{d}\theta})+(\lambda+\frac{\nu}{\sin^2{\theta}})\Theta=0$$となる。第1式は容易に$\Phi$について解くことができ、$$\Phi(\phi) = A\exp(i\nu^{\frac{1}{2}}\phi)+B\exp(-i\nu^{\frac{1}{2}}\phi)\quad(\nu\ne 0)\\
\Phi(\phi)=A+B\phi\quad(\nu=0)$$となる。$\Phi$,$\frac{\mathrm{d}\Phi}{\mathrm{d}\phi}$は定義域$0\sim2\pi$において連続であるのでこの条件のもとで$\Phi$は
$$\Phi_m = (2\pi)^{\frac{1}{2}}\exp(im\phi)$$となる。ここで$m$は$\nu=m^2$を満たし、正負の整数または0をとる。定数項は$Y$にとっての規格化定数である。
次に第2式について考える。
$$\frac{1}{\sin\theta}\frac{\mathrm{d}}{\mathrm{d}\theta}(\sin\theta\frac{\mathrm{d}\Theta}{\mathrm{d}\theta})+(\lambda+\frac{\nu}{\sin^2{\theta}})\Theta=0$$
$\psi=\cos\theta$とおくことによって
$$\frac{\mathrm{d}}{\mathrm{d}\psi}((1-\psi^2)\frac{\mathrm{d}\Theta}{\mathrm{d}\psi})+(\lambda+\frac{m^2}{1-\psi^2})\Theta=0$$
のように書き直すことができる。この式は二階の微分方程式であるので、2つの一次独立の解がある。$\psi=\pm 1$で解が存在するためには$\lambda=l(l+1)$とならなければならない。ただし$l$は正の整数または0である。これにより第二式は以下のように表すことができる。
$$\frac{\mathrm{d}}{\mathrm{d}\psi}((1-\psi^2)\frac{\mathrm{d}\Theta}{\mathrm{d}\psi})+(l(l+1)+\frac{m^2}{1-\psi^2})\Theta=0$$
これは有名な微分方程式の形となっており、この解をLegendreの陪多項式と呼び$\Theta$は
$$\Theta_l^{m}(\xi)=\frac{1}{2^{m}m!}(1-\xi^2)^{m/2}\frac{d^{m+l}}{d\xi^{m+l}}(\xi^2-1)^{l}\\
=(1-\xi^2)^{m/2}\frac{d^{m}}{d\xi^{m}}P_l(\xi)$$
とかける。(一般的にこの式の解は$l,m$を上記のように明示的に書くのでここでもその記法に習い$\Theta$を$\Theta_l^{m}$と書いた。)ここで$P_l$は以下のような形となり、Legendreの多項式と言う。
$$P_{l}(\xi)=\frac{1}{2^l l!}\frac{d^l}{d\xi^l}(\xi^2-1)^l$$
すぐ後にわかるがLegendreの陪多項式の規格化定数は$Y(\theta,\phi)$に$\Theta,\Phi$を代入したのちに求めたほうが都合が良いのでここでは$N_{lm}$とする。
早速$Y(\theta,\phi)$に代入して求める。$Y(\theta,\phi)$は
$$Y(\theta,\phi)=N_{lm}\Theta_l^{m}\Phi_m$$のように書くことができる。規格直交性をもとに規格定数を求める。$l$を選択することによって$m$は$(2l+1)$通りの値をとるので$l$は縮退しているが、$\Phi_m$によって$m$を一意に定めることによってこの縮退した関数も互いに直交するようになる。以上から
$$\int_0^\pi\int_0^{2\pi}Y_{lm}^*(\theta,\phi)Y_{\acute{l}\acute{m}}(\theta,\phi)\sin\theta\mathrm{d}\theta\mathrm{d}\phi=\int_1^1\int_0^{2\pi}Y_{lm}^*Y_{\acute{l}\acute{m}}\mathrm{d}\psi\mathrm{d}\phi$$
の値は$l\ne\acute{l}$または$m\ne\acute{m}$のとき0になる。$m\ne\acute{m}$のとき$l$とは無関係に$\phi$についての積分が0になる。このことより$\psi$に関する積分は$l\ne\acute{l}$,$|m|=|\acute{m}|$のとき0になる。つまり
$$\int_1^1P_l^mP_{\acute{l}}^{m}\mathrm{d}\psi$$を用いて$N_{lm}$を求めることができる。この積分を計算するためにLegendreの陪多項式の母関数を利用する。これは
$$T_m(\phi,s)=\frac{(2|m|)!(1-\psi^2)^\frac{|m|}{2}s^{|m|}}{2^{|m|}(|m|)!(1-2s\psi+s^2)^{|m|+\frac{1}{2}}} = \sum_{l=|m|}^{\infty}P_l^m(\psi)s^l$$
とかける。
$$\int_{-1}^1T_m(\psi, s)T_m(\psi,t)\mathrm{d}\psi\\
=\int_{-1}^1(\frac{(2|m|)!(1-\psi^2)^{\frac{|m|}{2}}}{2^{|m|}(|m|)!})^2\frac{s^{|m|}}{(1-2s\psi+s^2)^{|m|+\frac{1}{2}}}\frac{t^{|m|}}{(1-2t\psi+t^2)^{|m|+\frac{1}{2}}}\mathrm{d}\psi\\
=\sum_l\sum_{\acute{l}}s^lt^l\int_{-1}^1P_l^mP_{\acute{l}}^m\mathrm{d}\psi
$$
これを利用し、計算すると(煩雑な計算であるのでここでは結果のみ示す)、積分の結果(母関数の内積ではなく、Legendremの陪多項式の内積)は$l\ne\acute{l}$のときはゼロ、$l=\acute{l}$のときは$[2/(2l+1)][(l+|m|)!/(l-|m|)!]$となるので$N_{lm}$はこの平方根の逆数をとることで得られる。つまり、
$$N_{lm}=[\frac{2l+1}{2}\frac{(l-|m|)!}{(l+|m|)!}]^{\frac{1}{2}}$$
これより得られる$Y_{lm}(\theta,\phi)$は
$$Y_{lm}(\theta,\phi)=(-1)^{(m+|m|)/2}\sqrt{\frac{2l+1}{4\pi}\frac{(l-|m|)!}{(l+|m|)!}}P_l^{m}(\cos\theta)e^{im\phi}$$
となり、球面調和関数(Spherical harmonics)と言う。ここで記述した$P_l^{|m|}$はLegendreの陪多項式である。一般的に$\Theta$ではなく$P$を用いて描かれるのでそれに則ってこのようにした。

### 動経に関する計算
次に動経方向に関する方程式に関して考える。動軽方向の関数は以下のようであった。
$$-\frac{\hbar^2}{2m}(\frac{d^2\chi}{dr^2}-\frac{\lambda}{r^2}\chi)+V(r)\chi=\epsilon\chi$$
先ほどの議論にて$\lambda=l(l+1)$であることが分かった。だが$V(r)$についての形は$r$にのみ依存すること以外は全く決定されていない。今回の議論では水素原子中における電子に関して行っているので、核と電子間に働くクーロンポテンシャルのみ考えるとすると$$V(r)=-\frac{e^2}{4\pi\epsilon_0 r}$$
で$V(r)$は与えられる。
これらを代入すると先ほどの方程式は
$$-\frac{\hbar^2}{2m}\frac{\mathrm{d}^2\chi}{\mathrm{d}r^2}+\{\frac{\hbar^2}{2m}\frac{l(l+1)}{r^2}-\frac{e^2}{4\pi\epsilon_0 r}\}\chi=\epsilon\chi$$
とかける。ここで、ボーア半径$a_0=\frac{4\pi\epsilon_0\hbar^2}{me^2}=5.29177\times10^{-11}\mathrm{m}$を用いて、$\rho=\frac{r}{a_0},\eta=\frac{2(4\pi\epsilon_0)^2\hbar^2}{me^4}\epsilon$なる変数変換を行う。そうすると今求めるべく方程式は
$$\frac{\mathrm{d}^2\chi}{\mathrm{d}\rho^2}+\{\frac{2}{\rho}-\frac{l(l+1)}{\rho^2}\}\chi+\eta\chi=0$$となる。まず、この方程式の$\rho\to0$での様子について考えてみる。今$\chi$を$\rho$についての冪級数展開$$\chi=\rho^\alpha \sum_{i}a_i\rho^i$$で表すことができるとする。($a_0\ne0$)今$\chi\to0$を考えているので$\rho$の最低次のみを考えて、考えている方程式に代入すると$$a_0[\alpha(\alpha-1)-l(l+1)]=0$$となることがわかる。つまり$\alpha$は$\alpha=l+1,\alpha=-l$を満たすことが分かる。$\alpha=l+1$のとき$\chi$は$\chi\to0$で$\chi=a_0\rho^{l+1}$となる。また、$\alpha=-l$のときは$\chi=a_0/\rho^{l-1}$となり、ゼロに収束しないので解として不適切である。よって$\rho\to0$のとき$\chi=\rho^{l+1}$である。次に$\rho\to\infty$について考える。このとき方程式は$$\frac{\mathrm{d}^2\chi}{\mathrm{d}\rho^2}=-\eta\chi$$となる。この解は$\chi=\exp(\pm i\eta^{1/2}\rho))$となる。$\eta$は$\frac{1}{n^2}$のような飛び飛びな値を取るので、$\chi=\exp(-\rho/n)$であることが分かる。これまでの議論を甘味するとと$\chi$は$\chi=\rho^{l+1}e^{-\frac{\rho}{n}}v_{nl}(\rho)$の形で表される。方程式に代入すると、
$$\rho\frac{\mathrm{d}^2}{\mathrm{d}\rho^2}v_{lm}+(2l+2-\rho)\frac{\mathrm{d}}{\mathrm{d\rho}}v_{lm}+(n-l+1)v_{lm}$$
となり、この形はLaguerreの陪多項式の形となっており、この解は$$L_n^k(x) = \sum_{m=0}^n(-1)^m\frac{(n+k)!}{(n-m)!(k+m)!m!}x^m$$のようにかける。よって$\chi$を求めることができ、$R_n^l$は$\rho^le^{\frac{\rho}{n}}L_{n+l}^{2l-1}(\rho)$を規格化したものとなる。これは球面調和関数の規格化定数を導出した時と同様に求めることができて、$$R_n^l(r) = \sqrt{(\frac{2Z}{na_0})^3\frac{(n-l-1)!}{2n(n+l)!}}(\alpha r)^l\mathrm(e)^{-\alpha r/n}L_{n＋l}^{2l+1}(\alpha r)$$となる。
## 水素原子における電子の軌道
波動関数を変数分離させ、得られた関数$R(r),Y(\theta,\phi)$について考察した。$\psi(r,\theta,\phi)=R_n^l(r)Y_l^m(\theta,\phi)$であるのでn,l,mを指定することで波動関数を求めることができる。

## 参考文献
シッフ 新版 量子力学(上) 井上健(訳)
量子力学(Ⅰ) 小出昭一郎