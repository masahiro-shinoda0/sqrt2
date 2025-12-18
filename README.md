# sqrt2
ニュートン法で $`\sqrt{2}`$ の近似値を求める


## ニュートン法
まずは一般的な関数で考えることにする。以下のような関数 $`y=f(x)`$ を考える。\
$`f(x)`$ は，$`x=a \quad(a>0)`$において，$`f'(a)>0, \quad f''(a)>0`$であり，$`f(a-\varepsilon) \cdot f(a+\varepsilon)<0 \quad(\varepsilon は微小量)`$を満たすものとする。つまり， $`f(x)`$ は $`x=a`$ で $`x`$軸と交わり，そのときの傾きは正である。中間値の定理にさらに厳しい制約を適応したものでもある。二階微分が正としたのは，単にグラフを見やすくするためであり，数式的な意味はない。

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

したがって，$`\sqrt{2}`$ は，$`f( \sqrt{2} )=0`$ となる関数 $`f(x)`$ について，$`x`$軸と交わる交点の座標 $`A_n`$ についての漸化式を立てたときの，$`A_n`$ の極限値である。

## $$\sqrt{2}$$ を求める
次に，実際に漸化式を解いて $`\sqrt{2}`$ を求める。まず，$`a=\sqrt{2}`$となるようにうまく関数 $`f(x)`$ を設定する。ここでは整数係数の多項式で簡単なものとして，$`f(x)=x^2-2`$ を考える。$`x^2-2=(x-\sqrt{2})(x+\sqrt{2})`$ と因数分解できるため，$`x=\pm \sqrt{2}`$ を解に持ち，適する。$`f'(x)=2x`$ であり，適当に $`x=2 \quad (2>\sqrt{2})`$ とすると，漸化式は以下のようになる。

<p align="center">
  $A_{n+1}=A_n-\frac{{A_n}^2-2}{2A_n}$
</p>

これを変形すると，$`A_{n+1}=\frac{A_n}{2}+\frac{1}{A_n}`$となる。なお，実際にプログラム中に書く更新式は，`t = t/2 + 1/t` などとするのがよい。

### 漸化式を解く
極限値を $`\alpha=\lim_{n\to \infty} A_n`$ とし，漸化式に代入すると，$`\alpha=\frac{\alpha}{2}+\frac{1}{\alpha}`$となり，これを解くと，$`\alpha=\sqrt{2}`$ となる。

#### 解法1 (はさみうちの原理)
もとの漸化式を以下のように変形する。

<p align="center">
  $A_{n+1}-\alpha=\frac{1}{2}(A_n-\alpha)+(\frac{1}{A_n}-\frac{1}{\alpha})$
</p>

次に，すべての自然数 $`n`$ に対して，$`A_n>\sqrt{2}`$ であることを，数学的帰納法を用いて証明する。
##### (I)
$`n=1`$ のとき。このとき，$`A_1 = 2 > \sqrt{2}`$ であるから，みたす。

##### (II)
$`n=k`$ のとき，$`A_k>\sqrt(2)`$ であると仮定すると，$`n=k+1`$ のとき，

<p align="center">
  $A_{k+1}-\sqrt{2} = A_k-\sqrt{2}-\frac{{A_k}^2-2}{2A_k} = A_k-\sqrt{2}-\frac{(A_k-\sqrt{2})(A_k+\sqrt{2})}{2A_k} = (A_k-\sqrt{2})(1-\frac{A_k+\sqrt{2}}{2A_k}) = (A_k-\sqrt{2})^2 \cdot \frac{1}{2A_k} > 0$
</p>

よって，$`n=k+1`$ のときもみたす。

(I), (II)より，すべての自然数に対して，$`A_n>\sqrt{2}`$ であることが示された。

上の結果より，$`A_n>\alpha=\sqrt{2}`$ ，よって$`\frac{1}{A_n}-\frac{1}{\alpha}<0`$であるから，以下の不等式を得る。

<p align="center">
  $|A_{n+1}-\alpha|<\frac{1}{2}|a_n-\alpha|$
</p>

繰り返し適用すると，

<p align="center">
  $|A_n-\alpha| < \frac{1}{2}|a_{n-1}-\alpha| < (\frac{1}{2})^2|a_{n-2}-\alpha| < \dots < (\frac{1}{2})^{n-1}|a_1-\alpha|$
</p>

よって，はさみうちの原理より，$`\lim_{n\to \infty} A_n = \sqrt{2}`$

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


### 計算機で求める
以下に疑似コードを挙げる。

```text
t = 2
Input n

for i : 1 to n
  t = t/2 + 1/t
end

return t
```

実際に`C++`でプログラムを作成し，実行した。`sqrt2.cpp`である。

結果は以下のようであった。

```text
Input n : 10
Answer is 1.41421
```

`n=10`ほどで十分な近似値が得られている。収束が速いことは，ニュートン法が二次収束であることが関係している。\
また，このコードのままでは小数点第五位までしか出せない。`C++`ではなく，`C`を使って，`printf("Answer is %10lf\n, t")`などとすると良い。`sqrt2.c`を追加予定。

追記：`github`の環境では`LaTeX`があまり適さないので，`pdf`を`math.pdf`などとして作り，そこに数式をまとめることとする。`word`を用いてグラフを作成し追記するのも良い。`Qiita`でも良いかもしれない。
