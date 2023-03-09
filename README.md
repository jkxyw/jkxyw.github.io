![Image](https://pic4.zhimg.com/80/v2-8acdbe49c2318087203d642c29a69693.png)

# 对Stone-Weierstrass定理的探讨

3/9

内容来自 Walter Rudin《数学分析原理》第七章函数序列与函数项级数，但并不是完全抄书，实际上是我自己思绪的一种整理吧。现在还没有找到一个比较符合我喜好文章的排版结构，处于尝试阶段，还请多批评。
另一方面，Stone-Weierstrass定理是一个大工程，可能还有一些东西会再写一篇文章来讨论。
最近在看交响诗篇，好看的捏，放一张截图。

----------------

### Weierstrass的逼近

> $\textbf{Theorem(Weierstrass).}\quad$ 如果 $f$ 是 $[a,b]$ 上的一个连续实函数，那么便有实多项式 $P_n$ 的序列使得
> $$
> \lim\limits_{n\to \infty} P_n(x) = f(x)
> $$
> 
> 在 $[a,b]$ 上一致地成立，对于连续复函数也可以用复多项式逼近

这是 $\text{Weierstrass}$ 最早发现的逼近定理的形式。

**证明 :** 不失一般性地假定 $[a,b] = [0,1]$ 并且假设 $f(0) = f(1) = 0$ ，否则令 $$
g(x) = f(x) - f(0) - x[f(1)-f(0)]\quad (0\le x\le 1)$$

我们再补充定义 $f$ 在 $[0,1]$ 以外地区间上取 $0$ 那么该函数在实轴上一致连续。

取
$$
Q_n(x) = \frac{(1-x^2)^n}{\int_{-1}^1 (1 - x^2)^n \,\mathrm{d}x}
$$

现在令
$$
P_n(x) = \int_{0}^1 f(t) Q_n(t-x) \,\mathrm{d}t
$$

注意到这样构造出来的 $P_n(x)$ 是关于 $x$ 多项式。虽然这是一个显然的结论，但是对卷积不熟悉的人可能会产生一定的困惑，所以这里详细展开一下：事实上注意到 $x$ 是变量，所以把 $Q_n$ 写成关于 $x$ 的多项式：
$$
\begin{aligned}
P_n(x) &= \int_{0}^1 f(t) Q_n(t-x) \,\mathrm{d}t \\
&= \int_{0}^1 f(t) \sum\limits_{k = 0} a_k(t) x^k \,\mathrm{d}t\\
&= \sum\limits_{k = 0} \left[\int_{0}^1 f(t) \sum\limits_{k = 0} a_k(t) \,\mathrm{d}t\right]x^k
\end{aligned}
$$

于是我们就可以试图证明 $P_n$ 逼近 $f$ ，为了完成这一点我们需要一些小小的铺垫，对于任取的 $\varepsilon > 0$ 由函数的连续性取得 $\delta > 0$ 使得 $|y - x| < \delta$ 时 $f(y) > f(x) - \frac{\varepsilon}{2}$ 。同时假设 $M = \sup |f(x)|$

为了完成这个证明我们现在还需要铺垫 $Q_n$ 的性质，也就是估计 $\int_{-1}^1 (1 - x^2)^n \,\mathrm{d}x$ 的数量级：
$$
\begin{aligned}
\int_{-1}^1 (1 - x^2)^n \,\mathrm{d}x &= 2\int_0^1(1- x^2)^n\,\mathrm{d}x\\
&\ge 2 \int_0^{\frac{1}{\sqrt n}} (1 - x^2)^n \,\mathrm{d}x\\
&\ge 2 \int_0^{\frac{1}{\sqrt{n}}} (1 - nx^2) \,\mathrm{d}x\\
&=\frac{4}{3\sqrt{n}}
\end{aligned}
$$

这样就把 $Q_n(0)$ 数量级控制在了 $\sqrt{n}$ 。对于任意一个 $\delta$ 在邻域 $(-\delta,\delta)$ 之外有 
$$
Q_n(x) \le\sqrt n(1 - \delta ^ 2) ^n
$$

这也就是说在这个邻域之外 $Q_n(x)$ 一致收敛到 $0$ ，这样我们就能开始最后的逼近。
$$
\begin{aligned}
\left| P_n(x) - f(x) \right| &= \left| \int_{-1}^1  [f(x + t) - f(x)] Q_n(t) \,\mathrm{d}t\right|  \\
&\le \int_{-1}^1 |f(x + t) - f(x)|Q_n(t)\,\mathrm{d}t \\
&\le 4M\sqrt{n}(1 - \delta ^ 2) ^ n + \frac{\varepsilon}{2}
\end{aligned}
$$

这样对于足够大的 $n$ 上式小于 $\varepsilon$ ，这也就证明了本定理。

**评注&补充 :** 我刚刚看到这一段证明的时候我非常好奇选取这样的 $Q_n$ 的动机是什么呢？我个人认为 $\text{rudin}$ 在这个部分并没有把这个问题讲清楚。幸好我同时在读 $\text{stein}$ 的傅里叶分析导论，其中作者提出的 $\text{Good Kernal}$ 的概念在很大程度上解答了我的这个疑惑。实际上本定理的证明想法和 $\text{stein}$ 证明 $\text{Fourier}$ 级数收敛性时使用的方法如出一辙。

我们首先观察 $Q_n(x)$ 这个函数，会发现这个函数在 $0$ 点呈现"峰值"的样貌，$\text{stein}$ 书中用 $\text{peaky}$ 来形容这种性质。

![Image](https://pic4.zhimg.com/80/v2-1b8781df3394870ddf4cfd178ad485af)

于是这里我们阐述 $\text{Good Kernal}$ 的概念：对于任意一组卷积核 $K_n$ 如果有

$\text{(a)} $ $\frac{1}{2\pi}\int_{-\pi}^\pi K_n(x) \,\mathrm{d}x = 1$​
$\text{(b)} $ $\frac{1}{2\pi}\int_{-\pi}^\pi K_n(x) \,\mathrm{d}x$ 关于 $n$ 是有界的
$\text{(c)} $ 在任意一个邻域之外积分为零 $\int_{\delta\le|x|\le\pi}|K_n(x)|\,\mathrm{d}x \to 0$

那么我们就称之为好核。满足这样条件的"好核"具有**单位逼近性(approximation to identity)**，也就是说
$$
\lim\limits_{n\to \infty} (K_n* f)(x) = f(x)
$$

当然这些性质是基于对傅里叶分析的研究而提出的，不过其中的思想对于我们理解本定理的构造是有参考价值的，本题证明中的 $Q_n$ 就是构造了这样的一个具有类似好核性质的卷积核。

### Stone对Weierstrass的推广

首先给出一个原始逼近定理的推论，这个推论是接下来推广定理所需要的全部结论（也因此我们其实可以通过其他的路径去证明这个推广的定理）

> $\textbf{Corollary.}\quad$ 可以用多项式函数一致逼近 $f(x) = |x|$

现在我们知道，多项式能够一致地逼近任意连续函数，因此现在希望把多项式地一些能够使逼近成立的性质提取出来，我们希望探究怎么样的一族函数能够使得逼近成立。

> $\textbf{Definition.}\quad$ 我们称定义在集合 $E$ 上的复函数族 $\mathscr A$ 称为**代数**如果满足以下条件：
> $\ \text{ i)} $ 对于任意 $f,g\in\mathscr A$ 有 $f+g\in\mathscr A$
> $\text{ ii)} $ 对于任意 $f,g\in\mathscr A$ 有 $f g\in\mathscr A$
> $\text{iii)} $ 对于任意 $f\in\mathscr A$ 和常数 $c$ 有 $cf\in\mathscr A$
> 换言之就是满足对加法、乘法、数乘的封闭性。
>
> 如果族 $\mathscr A$ 中存在一列函数 $f_n$ 一致收敛到 $f$ 那么 $f$ 可以认为是 $\mathscr A$ 的一致极限函数（这个词是我自己造的，如有不当请批评）。如果所有一致极限函数都在 $\mathscr A$ 中那么称 $\mathscr A$ 是**一致闭的**。$\mathscr A$ 的一切一致极限函数构成的函数族被称为**一致闭包**。

显然所有多项式构成的集合就是一个代数，因此原始的定理可以被叙述成 $[a,b]$ 上的连续函数集是 $[a,b]$ 上的多项式集的一致闭包，我们接下来要探究的问题就是怎么样的一个代数他的一直闭包是全体连续函数。

仿照点集拓扑中的理论（读者自证不难），容易证明**一致闭包是一致闭的**。

接下来再追加几个关于函数族的定义

> $\textbf{Definition.}\quad$ 如果对于任意 $x_1,x_2\in E$ 存在一个函数 $f\in\mathscr A$ 使得 $f(x_1)\neq f(x_2)$ ，那么我们称 $\mathscr A$ 能**分离（区分）** $E$ 。如果对于任意 $x\in E$ 存在一个函数 $f\in\mathscr A$ 使得 $f(x) \neq 0$ 那么我们称 $\mathscr A$ **不在 $E$ 上消失**。

这两个关于函数族的条件看起来很弱，实际上通过简单的代数推导我们可以发现二者可以组合出较强的结论。

> $\textbf{Theorem.}\quad$ 设 $\mathscr A$ 是定义在集合 $E$ 上的函数的代数， $\mathscr A$ 能分离中的点并且在上不消失，那么对于任意的 $x_1,x_2\in E$ 和任意的常数 $c_1,c_2$ 一定存在一个 $f \in \mathscr A$ 使得
> $$
> f(x_1)=c_1,\ f(x_2)=c_2
> $$

**证明 :** $\mathscr A$ 中一定存在函数 $g,h,k$ 满足
$$
g(x_1)\neq g(x_2),\ h(x_1) \neq 0,\ k(x_2) \neq 0
$$

令 
$$
u = [g-g(x_1)]k, v = [g-g(x_2)]h
$$

最后取 $f = \frac{c_1v}{v(x_1)} + \frac{c_2u}{u(x_2)}$ 就可以满足条件

> $\textbf{Theorem(Stone).}\quad$ $\mathscr A$ 是紧集合 $K$ 上的实连续函数的代数，如果他能区分点并不消失，$\mathscr A$ 的一致闭包 $\mathscr B$ 由 $K$ 上的全体连续实函数构成。

$\text{rudin}$ 对这个定理的证明分成了四步

**第一步** 如果 $f\in\mathscr B$ 那么 $|f|\in\mathscr B$

对于任意的实数 $\varepsilon > 0$ 我们知道存在多项式 $p(x) = \sum\limits_{i = 0}^k a_i x^i$ 使得 
$$
|p(x) - |x|| <\varepsilon
$$

也就是 $\left| \sum\limits_{i = 0} ^ ka_if^i  - |f|\right|  <\varepsilon$ 一致地成立

我们又知道 $\sum\limits_{i = 0} ^ ka_if^i \in\mathscr B$ 因此我们就证明了 $|f|\in\mathscr B$ 

**第二步** 如果 $f, g\in\mathscr B$ 那么 $\max(f,g),\min(f,g)\in\mathscr B$

应用第一步的结论这是显然的，只需注意到
$$
\max(f,g) = \frac{f + g}{2}+\frac{|f-g|}{2}\\
\min(f,g) = \frac{f + g}{2}-\frac{|f-g|}{2}
$$

**第三步** 对任意的实连续函数 $f$ 以及一点 $x \in K$ ，对于任意的 $\varepsilon > 0$ ，便存在着一个函数 $g_x \in \mathscr B$ 满足 $g_x(x) = f(x)$ 并且
$$
g_x(t) > t - \varepsilon
$$

**第四步** 给定一个实连续函数 $f$ 和 $\varepsilon > 0$ ，那么存在一个函数 $h \in\mathscr B$ 使得
$$
|h(x) - f(x)| <\varepsilon
$$

### 问题与讨论
