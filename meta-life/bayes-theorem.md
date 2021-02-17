# 贝叶斯定理

## 定理

$$
\begin{aligned}\Pr(A|B)\times\Pr(B) &= \Pr(B|A)\times\Pr(A)\\
\Pr(A|B) &= \frac{\Pr(B|A)\times\Pr(A) }{\Pr(B)}\\
&= \frac{\Pr(B|A)\times\Pr(A) }{\Pr(B|A)\times\Pr(A) + \Pr(B| \lnot A)\times\Pr(\lnot A)}\end{aligned}
$$

其中：

- A 的先验：$$\Pr(A)$$
- A 的后验：$$\Pr(A|B)$$
- B 的先验：$$\Pr(B)$$
- B 的后验：$$\Pr(B|A)$$

## 事件 B 发生的总概率

$$
\begin{aligned}\Pr(B) &= \phantom{111} \Pr(A\cap B)\phantom{(1)} + \phantom{111}\Pr(\lnot A\cap B)\\
&= \overbrace{\Pr(B|A)\times\Pr(A)} + \overbrace{\Pr(B| \lnot A)\times\Pr(\lnot A)} \end{aligned}
$$

需要知道：

- A 的概率：$$\Pr(A)$$，$$\Pr(\lnot A)=1-\Pr(A)$$
- 如果 A 发生，那么 B 发生的概率：$$\Pr(B|A)$$
- 如果 A 不发生，那么 B 发生的概率：$$\Pr(B|\lnot A)$$

## 事件 B 发生了，那么事件 A 发生的概率？

$$
\begin{aligned}\Pr(A|B) &= \frac{\Pr(B|A)\times\Pr(A) }{\Pr(B)}\\
&= \frac{\Pr(B|A)\times\Pr(A) }{\Pr(B|A)\times\Pr(A) + \Pr(B| \lnot A)\times\Pr(\lnot A)} \\
&= \frac{\Pr(A\cap B)}{\Pr(A\cap B) + \Pr(\lnot A\cap B)}\end{aligned}
$$

所以**如果 $$\Pr(A)$$ （目标事件的发生概率） 非常小，那么即使 $$\Pr(B|A)$$ 非常大，$$\Pr(A|B)$$ 也可能很小。**

> 如果一个疾病比较罕见，那么你就不应该对阳性诊断太有信心。
> 
> 由此我联想到中国历史特殊时期的“抓特务”行动。“特务”这个工作的要求，其实贵在精而不在多，再说国民党也没那么多钱养，真正的特务其实是很少的。如果我们看到一个人长得像特务，说话走路也像特务，我们有多大把握说他就是特务呢？上面这个例子告诉我们，“误诊率”可能相当高。“抓特务”，最好的办法是冒出来一个抓一个，最可怕的办法是搞“人人过关”。如果你搞“人人过关”，必然是一大堆冤假错案！
>
>这就是冤假错案产生的数学原理，这也是为什么卡尔·萨根说“超乎寻常的论断需要超乎寻常的证据”。

Source: 智识分子. 万维钢. Part III. 贝叶斯定理的胆识.

## Trivia

![Modified Bayes' Theorem](https://imgs.xkcd.com/comics/modified_bayes_theorem_2x.png)

翻译：[修正贝叶斯定理 - XKCD 中文站](https://xkcd.in/comic?lg=cn&id=2059)
