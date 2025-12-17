# NewtonsMethods
ニュートン法で $`\sqrt{2}`$ の近似値を求める


## ニュートン法
関数 $`y=f(x)`$ を考える。$`f(x)`$ は，$`x=a \quad(a>0)`$において，$`f'(a)>0, \quad f''(a)>0`$であり，$`f(a-\varepsilon) \cdot f(a+\varepsilon)<0 \quad(\varepsilon は微小量)`$を満たすものとする。つまり， $`f`$ は $`x=a`$ で $`x`$軸と交わり，そのときの傾きは正である。中間値の定理にさらに厳しい制約を適応したものでもある。

このとき，$`x=t \quad (t>a)`$ における接線は以下のように表される。
<p align="center">
  $y-f(t)=f'(t)(x-t)$ 
</p>

これを $`y=0`$ として $`x`$ について解くと，

<p align="center">
  $x=t-\frac{f(t)}{f'(t)}$
</p>
となる。

これより，漸化式を立てることができる。$`n=1,2,...`$として $`t`$ を $`n-1`$ 回更新したものを $`A_n`$とすると，以下の漸化式をみたす。

<p align="center">
  $A_{n+1}=A_n-\frac{f(A_n)}{f'(A_n)}$
</p>

ただし，$`A_1=t`$ である。また，$`\lim_{n\to \infty} A_n = a`$ となる。

## $$\sqrt{2}$$ を求める
まず，$`a=\sqrt{2}`$となるようにうまく関数 $`f`$ を設定する。ここでは整数係数の多項式で簡単なものとして，$`f(x)=x^2-2`$ を考える。$`x^2-2=(x-\sqrt{2})(x+\sqrt{2})`$ と因数分解できるため，$`x=\pm \sqrt{2}`$ を解に持ち，適する。$`f'(x)=2x`$ であり，適当に $`x=2 \quad (2>\sqrt{2})`$ とすると，漸化式は以下のようになる。

<p align="center">
  $A_{n+1}=A_n-\frac{{A_n}^2-2}{2A_n}$
</p>

これを変形すると，$`A_{n+1}=\frac{A_n}{2}+\frac{1}{A_n}`$となる。なお，実際にプログラム中に書く更新式は，`t = t/2 + 1/t` とするのがよい。

### 漸化式を解く
極限値を $`\alpha=\lim_{n\to \infty} A_n`$ とし，漸化式に代入すると，$`\alpha=\frac{\alpha}{2}+\frac{1}{\alpha}`$となり，これを解くと，$`\alpha=\sqrt{2}`$ となる。

#### 解法1
もとの漸化式を以下のように変形する。

<p align="center">
  $A_{n+1}-\alpha=\frac{1}{2}(A_n-\alpha)+(\frac{1}{A_n}-\frac{1}{\alpha})$
</p>

#### 解法2
もとの漸化式から，$`\sqrt{2}, -\sqrt{2}`$ をそれぞれ引いたものを考える。

<p align="center">
  $A_{n+1}-\sqrt{2}=\frac{{A_n}^2+2-2\sqrt{2}A_n}{2A_n} = \frac{(A_n-\sqrt{2})^2}{2A_n}$
</p>

同様にして，

<p align="center">
  $A_{n+1}+\sqrt{2}=\frac{{A_n}^2+2+2\sqrt{2}A_n}{2A_n} = \frac{(A_n+\sqrt{2})^2}{2A_n}$
</p>

辺々割ると，

<p align="center">
  $\frac{A_{n+1}+\sqrt{2}}{A_{n+1}-\sqrt{2}} = \frac{(A_n+\sqrt{2})^2}{(A_n-\sqrt{2})^2} = (\frac{A_n+\sqrt{2}}{A_n-\sqrt{2}})^2$
</p>

ここで，$`B_n=\frac{A_n+\sqrt{2}}{A_n-\sqrt{2}}`$ とおくと，$`B_{n+1} = {B_n}^2`$ である。両辺対数を取ると，$`\log{B_{n+1}} = 2\log{B_n}`$ となる。\
ここで，$`C_n=\log{B_n}`$ とおくと，$`C_{n+1} = 2C_n`$ である。$`C_1=\log{B_1}=\log{\frac{A_1+\sqrt{2}}{A_1-\sqrt{2}}}=\log{(3+2\sqrt{2})}`$ より，$`C_n`$ の一般項は，

<p align="center">
  $C_n = C_1 \cdot 2^{n-1} = \log{(3+2\sqrt{2})} \cdot 2^{n-1}$
</p>

よって，$`B_n`$ の一般項は，

<p align="center">
  $B_n = e^{C_n} = e^{\log{(3+2\sqrt{2})} \cdot 2^{n-1}} = (3+2\sqrt{2}) \cdot e^{2^{n-1}}$
</p>

よって，$`A_n`$ の一般項は，

<p align="center">
  $A_n = \sqrt{2} \cdot \frac{B_n+1}{B_n-1} = \sqrt{2} \cdot \frac{(3+2\sqrt{2}) \cdot e^{2^{n-1}}+1}{(3+2\sqrt{2}) \cdot e^{2^{n-1}}-1} = \sqrt{2} \cdot \frac{(3+2\sqrt{2}) +e^{-2^{n-1}}}{(3+2\sqrt{2}) -e^{-2^{n-1}}}$
</p>

したがって，$`\lim_{n\to \infty} A_n = \sqrt{2} \cdot \frac{3+2\sqrt{2}+0}{3+2\sqrt{2}-0} = \sqrt{2}`$
