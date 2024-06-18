# 范化与范式

#### 函数依赖

函数依赖：关系表$R$ 中取两个子集$\alpha$ 和$\beta$ ，如果对于$R$ 中任意两个元组$t_1$ 和$t_2$ 在$\alpha $ 各属性相等的时候也满足$\beta$属性都相等，则记$\alpha \rightarrow \beta$。$（t_1[\alpha]=t_2[\alpha]\Rightarrow t_1[\beta]=t_2[\beta]）$

#### 超键与候选键

超键：当且仅当$K\rightarrow R$时，才认为$K$是$R$的超键。

候选键：$K\rightarrow R$且不存在任何一个$K$的子集$K_i$使得$K_i\rightarrow R$

#### 平凡函数依赖

平凡函数依赖：如果$\beta \subseteq \alpha$，我们认为$\alpha\rightarrow\beta$是平凡的。

#### 无损分解

无损分解：将一个关系表$R$拆分成两个关系表$R_1$和$R_2$，如果$\Pi_{R_1}\bowtie \Pi_{R_2}=R$，则认为是无损分解；如果$R\subset \Pi_{R_1}\bowtie \Pi_{R_2}$，则是有损分解。

无损分解的充分条件：$R_1 \cap R_2\rightarrow R_1或 R_1\cap R_2 \rightarrow R_2$。也就是说证得其一可知其为无损分解。

#### 函数依赖的闭包

函数依赖的闭包：给定一个函数依赖的集合$F$，将所有能从$F$中推出的函数依赖构成的集合记作该集合的闭包$F^+$。

当且仅当关系$R$中的一个函数依赖存在于闭包$F^+$中时，它才成立。

函数依赖的闭包的获取方法：阿姆斯特朗公理

- 自反律：如果$\beta\subseteq\alpha$，则$\alpha\rightarrow\beta$。
- 增补律：如果$\alpha\rightarrow\beta$，则$\gamma\alpha\rightarrow\gamma\beta$
- 传递律：如果$\alpha\rightarrow\beta$且$\beta\rightarrow\gamma$，则$\alpha\rightarrow\gamma$。

还有其它几个规则，可以由上面这些推出：

- 合并律：如果$\alpha\rightarrow\beta$且$\alpha\rightarrow\gamma$，则$\alpha\rightarrow\beta\gamma$。
- 分解律：如果$\alpha\rightarrow\beta\gamma$，则$\alpha\rightarrow\beta$且$\alpha\rightarrow\gamma$。
- 伪传递率：如果$\alpha\rightarrow\beta$且$\gamma\beta\rightarrow\delta$，则$\alpha\gamma\rightarrow\delta$。

需要注意的是，这里面$\alpha\beta$并不是集合意义上的交集，而是并集。

具体算法：每轮循环中，先使用自反律和增补律，然后使用传递率。

#### 属性集合的闭包

属性集合的闭包：将集合$\alpha$在函数依赖集合$F$下的闭包记作$\alpha^+$。

计算流程：

- 初始化：结果集合$result$初始化为$\alpha$。
- 循环以下过程：如果$F$中某个函数依赖$\beta\rightarrow\gamma$满足$\beta$是$result$的子集，则将$\gamma$添加到$result$中。

判断属性集合$\alpha$是否为超键的方式：判断其闭包$\alpha^+$是否与关系集合$R$等价。

判断函数依赖$\alpha\rightarrow\beta$是否成立（函数依赖是否在函数的闭包中）的方式：判断$\beta\subset \alpha^+$是否成立。

函数依赖的闭包的获取方法2：对于$R$的每一个子集$\gamma$，求它的闭包$\gamma^+$，且对每一个$\gamma^+$的子集$S$，输出一个函数依赖$\gamma\rightarrow S$。所有输出的交集即是函数依赖的闭包。

#### 依赖保持和它的验证方法

依赖保持：在验证分解后的子关系上的函数依赖时，无需进行笛卡尔积即可进行验证。（一个说法是，任意函数依赖中的所有属性都必须在同一个子关系中。）

依赖保持的新定义：将一个表格$R$拆分成$R_1, R_2,...,R_n$，又将$F^+$中只包含$R_i$中属性的函数依赖的集合称作“$F$在$R_i$上的***限定***”$F_i$，则当$(F_1\cup F_2\cup ...\cup F_n)^+=F^+$时，$F$中所有依赖都被$F'$逻辑蕴含，从而实现了依赖保持。

一种避免计算$F^+$的验证依赖保持的方法：

- 初始时刻$result=\alpha$
- 不断重复以下过程：对于每个$R_i$，$t=(result\cap R_i)^+\cap R_i$，$result=result\cup t$。（这里计算闭包使用的是整个$F$）
- 当$result$没有变化时，如果$result$包含$\beta$中的所有属性，则$\alpha\rightarrow\beta$得到保持。

这个不断重复的过程其实相当于计算$F_i$下的$result$闭包，对每个$R_i$进行重复后得到$F'$下的$result$闭包。

#### 无关属性

无关属性：在函数依赖集合$F$中的某个函数依赖中，删去之后不会影响$F^+$的属性。

无关属性的判定：对于一个函数依赖$\alpha\rightarrow\beta$，

如果$A\in \alpha$且根据$F$可以推出$(F-\{\alpha\rightarrow\beta\})\cup\{(\alpha-A)\rightarrow\beta\}$，则认为A是无关属性；如果$A\in \beta$且根据$(F-\{\alpha\rightarrow\beta\})\cup\{\alpha\rightarrow(\beta-A)\}$可以推出$F$，则认为A是无关属性。

上面这个“可以推出”判断起来比较复杂，可以通过判断“属性的闭包是否包含新属性”来代替。

检验$A\in \alpha$是否是无关属性：只需检查$(\alpha-A)\rightarrow\beta$是否可以从$F$中推断出（成立）即可。使用$F$计算$(\alpha-A)^+$，如果$\beta\subset (\alpha-A)^+$则得证。

检验$A\in \beta$是否是无关属性：只需检查从$\beta$中去除A之后还能否推出$\alpha\rightarrow A$。使用$F'=(F-\{\alpha\rightarrow\beta\})\cup\{\alpha\rightarrow(\beta-A)\}$计算$\alpha$的新闭包$\alpha^+$，如果$A\in \alpha^+$则得证。

#### 正则覆盖

正则覆盖：一个函数集合$F$的正则覆盖$F_c$满足如下条件：

- $F$可以推出$F_c$
- $F_c$可以推出$F$
- $F_c$中的任何函数依赖都不包含无关变量
- $F_c$中任意两个函数依赖的左侧都两两不同。

正则覆盖的计算方法：

- 初始时设$F_c=F$
- 将所有形如$\alpha\rightarrow\beta_1$和$\alpha\rightarrow\beta_2$合并为$\alpha\rightarrow\beta_1\beta_2$
- 在$F_c$中遍历各函数依赖，如果发现一个无关属性，则将其删除。但是每个循环只删除一个。
- 重复以上过程，直到$F_c$不再发生变化。



---

## BCNF

BC范式（BCNF）：如果$F^+$中的所有函数关系$\alpha \rightarrow \beta$都满足：

- $\alpha\rightarrow\beta$是平凡的（即$\beta\subset\alpha$）
- 或者$\alpha$是关系R的超键

则认为这个关系表$R$满足BCNF。当$F^+$是空集的时候，也认为该关系表满足BCNF。

$F^+$可以通过将属性随机组合来判断是否存在函数依赖。

拆分关系$R$以满足BC范式：如果关系$R$中$\alpha\rightarrow\beta$不满足BCNF，则将$R$分成$\alpha\cup\beta$和$R-(\beta-\alpha)$。

#### BCNF的检测方法

检查$\alpha\rightarrow\beta$是否违反BCNF：如果不是平凡函数依赖，则计算$\alpha^+$，当其为关系$R$的超键时认为不违反。

简化的检查方法：只检查一个给定的函数集合$F$是否满足BCNF，而不是$F^+$。不过在检测$R$的分解是否满足BCNF时不能用这个方法，容易漏检。

分解后的BCNF检测方法：

1. 遍历$F$在$R_i$上的限定（$F^+$中只包含$R_i$中属性的函数依赖的集合）中的所有函数依赖，测试是否满足BCNF。
2. 或使用原有的函数依赖$F$。对于任意一个属性子集$\alpha \subseteq R_i$，验证$\alpha^+$不包括$R_i-\alpha$中的任何属性或包括$R_i$中的所有属性。（前者对应BCNF中的“平凡”条件，后者对应“超键”条件。）如果BCNF被某个函数依赖$\alpha\rightarrow\beta$打破，则一定存在一个$\alpha\rightarrow(\alpha^+-\alpha)\cap R_i$在$R_i$上存在。

#### BCNF的分解算法

BCNF分解算法：

- 给结果集合赋初值：$result=\{R\}$（注意这是一个关系表的集合）
- 计算$F^+$
- 如果$result$中存在一个$R_i$不满足BCNF，则找到其中一个违背BCNF且$\alpha\cap\beta=\varnothing$的函数依赖$\alpha\rightarrow\beta$，将$result$更新为$(result-R_i)\cup (R_i-\beta)\cup(\alpha,\ \beta)$（即，从$result$中去掉$R_i$，然后向其中添加$R_i-\beta$和$(\alpha,\beta)$）。循环执行这一步。

## 3NF

三范式（3NF）：如果$F^+$中的所有函数关系$\alpha \rightarrow \beta$都满足：

- $\alpha\rightarrow\beta$是平凡的（即$\beta\subset\alpha$）
- 或者$\alpha$是关系R的超键
- 或者$\beta-\alpha$中的每个属性都包含在$R$的某个候选键中

则认为这个关系表$R$满足3NF。

#### 3NF的检测方法

3NF检测方法：

- 只需检测$F$中的函数依赖而非$F^+$
- 使用属性集合的闭包检测对于每个函数依赖$\alpha\rightarrow\beta$，$\alpha$是否为超键。
- 如果$\alpha$不是超键，检测$\beta$中的每个属性是否包含在$R$的某个候选键中。

#### 3NF的分解算法

3NF分解算法：

- 获得$F$的正则覆盖$F_c$
- 初始化$i=0$
- 对于$F_c$中的每个函数依赖$\alpha\rightarrow\beta$，如果在$1\leq j\leq i$中没有任何一个关系$R_j$包含$\alpha\beta$，则$i$自增1，添加$R_i=\alpha\beta$；
- 如果在$1\leq j\leq i$中没有任何一个关系$R_j$包含$R$的候选键，则$i$自增1，添加$R_i=R的任意一个候选键$；
- 如果某个关系包含了另一个关系，则删除被包含的冗余关系；
- 得到分解后的$R_i$的集合



或者用一种更接近自然语言的方法描述：

初始情况下，分解后的关系表构成的集合为空集。对于$F$的正则覆盖中的每个关系$\alpha\rightarrow\beta$，如果没有任何一个分解后的关系表包含$\alpha\beta$，则将其作为一个分解后的关系表添加到集合中。遍历结束后，如果没有任何一个分解后的关系表包含$R$中的任意一个候选键，则选择一个候选键作为一个分解后的关系表添加到集合中。最后，删除重复的关系表。

---
## 多值依赖
多值依赖：将$R$的属性分为$\alpha$，$\beta$和$R-\alpha-\beta$三部分，如果对于任意一对元组$t_1和t_2$，存在$t_3和t_4$满足：

$$
t_1[\alpha]=t_2[\alpha]=t_3[\alpha]=t_4[\alpha]\\

t_1[\beta]=t_3[\beta]\\

t_2[\beta]=t_4[\beta]\\

t_1[R-\alpha-\beta]=t_4[R-\alpha-\beta]\\

t_2[R-\alpha-\beta]=t_3[R-\alpha-\beta]\\
$$

则认为$\alpha\rightarrow\rightarrow\beta$，同时有$\alpha\rightarrow\rightarrow R-\alpha-\beta$。

注意：如果有$\alpha\rightarrow\beta$则一定有$\alpha\rightarrow\rightarrow\beta$。

多值依赖的闭包：如果记函数依赖和多值依赖的集合为$D$，则将所有$D$逻辑蕴含的函数依赖和多值依赖的集合称为多值依赖的闭包$D^+$。可以根据其二者的定义计算出多值依赖的闭包。具体规则不做展开。

平凡多值依赖：$\alpha\cup\beta=R$或者$\beta\subset \alpha$。

## 第四范式

第四范式（4NF）：所有$D^+$中的形如$\alpha\rightarrow\rightarrow\beta$的多值依赖满足以下两个条件之一：$\alpha\rightarrow\rightarrow\beta$是平凡的，或者$\alpha$是$R$的一个超键。

如果一个关系符合第四范式，它一定符合BCNF。

$D$在集合$R_i$上的限定$D_i$：包含$D^+$中所有只含$R_i$中属性的函数依赖或者所有形如$\alpha\rightarrow\rightarrow\beta\cap R_i$的多值依赖，其中$\alpha \subseteq R_i$且$\alpha\rightarrow\rightarrow\beta\in D^+$。

4NF分解算法：与BCNF的很像

- 给结果集合赋初值：$result=\{R\}$（注意这是一个关系表的集合）
- 计算$D^+$，并用$D_i$表示$D$在集合$R_i$上的限定
- 如果$result$中存在一个$R_i$不满足4NF，则找到其中一个违背4NF且$\alpha\cap\beta=\varnothing$的多值依赖$\alpha\rightarrow\rightarrow\beta$，将$result$更新为$(result-R_i)\cup (R_i-\beta)\cup(\alpha,\ \beta)$（即，从$result$中去掉$R_i$，然后向其中添加$R_i-\beta$和$(\alpha,\beta)$）。循环执行这一步。
