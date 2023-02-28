# 贝叶斯定理

## 形式一：两个事件之间的关联

`$$
\begin{aligned}\Pr(A \mid B)\times\Pr(B) &= \Pr(B \mid A)\times\Pr(A)\\
\Pr(A \mid B) &= \frac{\Pr(B \mid A)\times\Pr(A) }{\Pr(B)}\\
&= \frac{\Pr(B \mid A)\times\Pr(A) }{\Pr(B \mid A)\times\Pr(A) + \Pr(B \mid  \lnot A)\times\Pr(\lnot A)}\end{aligned}
$$`

其中：

- A 的先验概率：`$\Pr(A)$`
- A 的后验概率：`$\Pr(A \mid B)$`
- B 的先验概率：`$\Pr(B)$`
- B 的后验概率：`$\Pr(B \mid A)$`


### 事件 B 发生的总概率

`$$
\begin{aligned}\Pr(B) &= \phantom{111} \Pr(A\cap B)\phantom{(1)} + \phantom{111}\Pr(\lnot A\cap B)\\
&= \overbrace{\Pr(B \mid A)\times\Pr(A)} + \overbrace{\Pr(B \mid  \lnot A)\times\Pr(\lnot A)} \end{aligned}
$$`

需要知道：

- A 的先验概率：`$\Pr(A)$`，`$\Pr(\lnot A)=1-\Pr(A)$`
- 如果 A 发生，那么 B 发生的概率：`$\Pr(B \mid A)$`
- 如果 A 不发生，那么 B 发生的概率：`$\Pr(B \mid \lnot A)$`


### 事件 B 发生了，那么事件 A 发生的概率？

`$$
\begin{aligned}\Pr(A \mid B) &= \frac{\Pr(B \mid A)\times\Pr(A) }{\Pr(B)}\\
&= \frac{\Pr(B \mid A)\times\Pr(A) }{\Pr(B \mid A)\times\Pr(A) + \Pr(B \mid  \lnot A)\times\Pr(\lnot A)} \\
&= \frac{\Pr(A\cap B)}{\Pr(A\cap B) + \Pr(\lnot A\cap B)}\end{aligned}
$$`

所以**如果 `$\Pr(A)$` （目标事件的发生概率） 非常小，那么即使 `$\Pr(B \mid A)$` 非常大，`$\Pr(A \mid B)$` 也可能很小。**

> 如果一个疾病比较罕见，那么你就不应该对阳性诊断太有信心。
> 
> 由此我联想到中国历史特殊时期的“抓特务”行动。“特务”这个工作的要求，其实贵在精而不在多，再说国民党也没那么多钱养，真正的特务其实是很少的。如果我们看到一个人长得像特务，说话走路也像特务，我们有多大把握说他就是特务呢？上面这个例子告诉我们，“误诊率”可能相当高。“抓特务”，最好的办法是冒出来一个抓一个，最可怕的办法是搞“人人过关”。如果你搞“人人过关”，必然是一大堆冤假错案！
>
> 这就是冤假错案产生的数学原理，这也是为什么卡尔·萨根说“超乎寻常的论断需要超乎寻常的证据”。
>
> ~ 智识分子. 万维钢. Part III. 贝叶斯定理的胆识.

---

> [Sagan standard - Wikipedia](https://en.wikipedia.org/wiki/Sagan_standard):
> 
> "Extraordinary claims require extraordinary evidence" (ECREE)


## 形式二：通过信号区分多种情况（贝叶斯更新）

`$$
\Pr(\theta_A \mid s) = \frac{\Pr(\theta_A)\times \Pr(s \mid \theta_A)}{\Pr(\theta_A)\times \Pr(s \mid \theta_A) + \Pr(\theta_B)\times \Pr(s \mid \theta_B)}
$$`

其中：

- 可能出现的情况（例如是否生病）：`$\theta_A$`（生病）， `$\theta_B$`（健康）
- 观察到的信号（例如检测）：`$s$`（检测为阳性）
- 分母为 `$s$` 的全概率公式

需要知道：

- 情况的先验：`$\Pr(\theta_A)$$（得病率），$$\Pr(\theta_B)$`
- 信号的准确度：`$\Pr(s \mid \theta_A)$$（灵敏度），$$\Pr(s \mid \theta_B)$`（1 - 特异度）


### 同样信号时不同情况的比值比，及线性形式（log odds form）

`$$
\begin{aligned}\frac{\Pr(\theta_A \mid s)}{\Pr(\theta_B \mid s)}
&= \frac{\frac{\Pr(\theta_A)\times \Pr(s \mid \theta_A)}{\Pr(\theta_A)\times \Pr(s \mid \theta_A) + \Pr(\theta_B)\times \Pr(s \mid \theta_B)}}{\frac{\Pr(\theta_B)\times \Pr(s \mid \theta_B)}{\Pr(\theta_A)\times \Pr(s \mid \theta_A) + \Pr(\theta_B)\times \Pr(s \mid \theta_B)}} \\
&= \frac{\Pr(\theta_A)\times \Pr(s \mid \theta_A)}{\Pr(\theta_B)\times \Pr(s \mid \theta_B)}\end{aligned}
$$`

两边取自然对数：

`$$
\log\left(\frac{\Pr(\theta_A \mid s)}{\Pr(\theta_B \mid s)}\right) = \log\left(\frac{\Pr(\theta_A)}{\Pr(\theta_B)}\right) + \log\left(\frac{\Pr(s \mid \theta_A)}{\Pr(s \mid \theta_B)}\right)
$$`

后验 = 先验 + 信号


<!-- 
### 拟贝叶斯更新

[Bayes Rule as a Descriptive Model: The Representativeness Heuristic* | The Quarterly Journal of Economics | Oxford Academic](https://academic.oup.com/qje/article-abstract/95/3/537/1934441?redirectedFrom=fulltext)

当一个人做决定不完全遵循贝叶斯时，可以建模为

`$$
\log\left(\frac{\Pr(\theta_A \mid s)}{\Pr(\theta_B \mid s)}\right) =  \alpha \cdot \log\left(\frac{\Pr(\theta_A)}{\Pr(\theta_B)}\right) + \beta(\theta) \cdot \log\left(\frac{\Pr(s \mid \theta_A)}{\Pr(s \mid \theta_B)}\right)
$$`

或

`$$
\log\left(\frac{\Pr(\theta_A \mid s)}{\Pr(\theta_B \mid s)}\right) =  \alpha \cdot \log\left(\frac{\Pr(\theta_A)}{\Pr(\theta_B)}\right) + \beta \cdot \log\left(\frac{\Pr(s \mid \theta_A)}{\Pr(s \mid \theta_B)}\right) + \gamma \cdot m(\theta)
$$`

其中：

- 对先验的重视程度：`$\alpha$`
- 对信号的重视程度：`$\beta$`
- 额外动机：`$\beta(\theta)$$或$$\gamma \cdot m(\theta)$`
 -->


## 娱乐

![[Modified Bayes' Theorem](https://www.explainxkcd.com/wiki/index.php/2059:_Modified_Bayes%27_Theorem)](https://imgs.xkcd.com/comics/modified_bayes_theorem_2x.png)

翻译：[修正贝叶斯定理 - XKCD 中文站](https://xkcd.in/comic?lg=cn&id=2059)
