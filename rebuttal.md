# Top-level answer (to all reviewers)

We thank all the reviewers for the insightful/constructive comments, and we are pleased that three reviewers pointed to thesignificance of our new setting in the context of transductive few-shot learning, and to the novelty of ourα-divergence method andDirichlet sampling. The borderline scores by reviewers maGM and W251 are stemming from requests of additional results/evaluations,which we provide below in this rebuttal.

# R1

We greatly appreciate the strong support to our work, and the positive comments on the significance of the results in the context of transductive few-shot learning and on the novelty/performance of the proposed $\alpha$-divergence optimization method. 

# R2

We thank the reviewer for the positive comments on the significance of our results, on the thorough experiments, and on the novelty of both our $\alpha$-divergence optimization and Dirichlet-based sampling.

# R3

We thank the reviewer for his review and address his concerns point by point in what follows. Note that figures and tables indexed with a letter (e.g Fig. A) can be found in the following anonymous link: https://github.com/anonymous6496/rebuttal , while figures indexed with a number are references to figures in the main paper.


## Choice of imbalance / additional imbalance scenarios


1- *The authors use one $\boldsymbol{a}$ value for the Dirichlet distribution (lines 257-264) to model query set imbalance during evaluation. It might be appropriate to evaluate several distributions or vary the $\boldsymbol{a}$ in the Dirichlet distribution.*


In Fig. A (anonymous link provided) and Tables A and B (below), we provide additional results over the three benchmarks for different values of Dirichlet's 
parameter $\boldsymbol{a}$ for modeling the query set during testing, including $\boldsymbol{a}= 1\cdot\mathbb{1}_K$ (distributions sampled 
uniformly at random), $\boldsymbol{a}= 0.5\cdot\mathbb{1}_K$ (extreme imbalanced-distribution sampling, cf Fig. B) and different levels of class 
balance ($\boldsymbol{a}= 3\cdot\mathbb{1}_K$, $\boldsymbol{a}= 5\cdot\mathbb{1}_K$, $\boldsymbol{a}= 7\cdot\mathbb{1}_K$ and
$\boldsymbol{a}= 10\cdot\mathbb{1}_K$). In fact, for uniformly-random sampling ($\boldsymbol{a}= 1\cdot\mathbb{1}_K$) 
and imbalanced-distribution sampling ($\boldsymbol{a}= 0.5\cdot\mathbb{1}_K$), the performance of $\alpha$-TIM is even higher 
and the performances of several existing methods is more severely affected (by important margins), which further strengthen the message of our 
work (Thanks for bringing this!). From the plots, we can observe that $\alpha$-TIM outperforms significantly the other methods when we tend to
uniformly-random testing tasks ($\boldsymbol{a}= 1\cdot\mathbb{1}_K$), while remaining competitive/stable when we tend to balanced testing tasks (i.e., the Dirichlet parameter is increasing). These results illustrate the flexibility of $\alpha$-divergences, and are in line with the technical 
analysis we provided in section 5.2 and Fig. 2. 


2- *It is not clear why this distribution ($\boldsymbol{a}= 2.\cdot\mathbb{1}_K$) was picked over others.*

As for the choice we made in the paper, while the validation tasks are also uniformly-random ($\boldsymbol{a}= 1.\cdot\mathbb{1}_K$), our rationale behind choosing $\boldsymbol{a}= 2\cdot\mathbb{1}_K$ for the testing tasks was to reflect the fact that extremely imbalanced tasks (i.e., only one class is present in the task) less likely to happen in practical scenarios ( $\boldsymbol{a}= 2\cdot\mathbb{1}_K$ is illustrated in Fig. A, left).
However, we do fully agree with the reviewer that providing results for various values of $\boldsymbol{a}$ would be much more informative for readers. In particular, uniformly-random sampling ($\boldsymbol{a}= 1\cdot\mathbb{1}_K$), as in the prior works mentioned by the reviewer, is important to provide to readers. Generating imbalanced distributions is also informative, although one may argue that we are replacing a perfect-balance artefact with an imbalance artefact. We will add Fig. A (performance versus $\boldsymbol{a}$) to the paper, and the results for uniformly-random sampling to the main Table. 


3- *The class imbalance community uses a range of distributions, for example, step imbalance and linear imbalance (Buda et al., 2018), long-tail imbalance (Wang et al., 2018), and in few-shot previous work sampled uniformly at random [32,33,34,35], or a combination of these distributions [35].*

Finally, we would like to mention that, initially in the project, we considered the specific linear imbalance 
mentioned by the reviewer and the results/conclusions are quite consistent with Dirichlet's sampling 
with $\boldsymbol{a}=2\cdot\mathbb{1}_K$. However, we abandoned this in favor of introducing a more general Dirichlet sampling because it could 
also covers these settings and we did not want to replace a perfect-balance artefact with a specific imbalance artefact. As illustrated in Fig. C, both linear and step imbalance correspond to particular spots within the simplex, which are also covered by $\boldsymbol{a}=2\cdot\mathbb{1}_K$. We believe introducing more principled Dirichlet sampling to the few-shot 
literature is also an important contribution of our work, and which might be even very useful to the class-imbalance community.
        

## Performance of $\alpha$-TIM

4- *It could be interesting to show the correlation between $\alpha$ and $\boldsymbol{a}$ in a graph.*

 
We plot in Fig. D the optimal value of $\alpha$ (on validation) for different values of $\boldsymbol{a}$. We observe an expected behavior: As $\mathbf{a}$ increases (i.e the query sets in testing become more and more balanced), the optimal value of $\alpha$ decreases and tend to 1 (which approaches the standard mutual information), with a trend that closely matches $\alpha^*=\frac{\text{const.}}{a} + 1$. 


 5- *Correlation between $\alpha$ and the number of shots?*

 As illustrated in Fig. E, the behaviour for 10-shot and 20-shot is quite similar to 5-shot, with the performances reaching a plateau when $\alpha$ is bigger than a certain value.

 6- *What is $\alpha$-TIM performance on the balanced setting?*

 $\alpha$-TIM is a generalization of TIM, as when $\alpha \rightarrow 1$ (i.e., the $\alpha$-entropies tend to the Shannon entropies), $\alpha$-TIM tends to TIM. Therefore, in the standard setting, where optimal hyper-parameter $\alpha$ is obtained over validation tasks that are balanced (as in the standard validation tasks of the original TIM and the other existing methods), the performance of $\alpha$-TIM is the same as TIM. When $\alpha$ is tuned on balanced validation tasks, we obtain an optimal value of $\alpha$ very close to 1, and our $\alpha$-mutual information approaches the standard mutual information. We will add comments on this in the paper.  When the validation tasks are uniformly random, as in our new setting and in the performance plots we provide here, one can see that the performance of $\alpha$-TIM remains competitive when we tend to balanced testing tasks (i.e., when $a$ is increasing), but is significantly better than TIM when we tend to uniformly-random testing tasks ($a=1$). These results illustrate the flexibility of $\alpha$-divergences, and are in line with the technical analysis we provided in section 5.2.  

## Performance of $\alpha$-TIM

7- *Claim on recent studies [32, 33, 34, 35]:*

 We fully agree with the reviewer. In fact, we point this out in l.278-280, stating that inductive methods do not use the statistics of the query set at adaptation and are, therefore, unaffected by class imbalance. We also concede that the wording of l.121 was misleading, and we will modify it. "Even these works" should in fact read "Even [32]", as [32] evaluates both the popular MAML and a transductive variant  (transductive through the use of transductive batch normalization), which could be affected by changes in the query-set balance (as shown in Table B provided in this rebuttal). 

 8- *Reasoning behind removing $\lambda$ for Eq. 5? What is the performance when it is included and tuned ?*


As mentioned by Reviewer KiFQ, we wanted to maintain equal hyper-parameter tuning budget with TIM for fairer comparison. $\alpha$ and $\lambda$ hyper-parameters can be understood as two different ways of dealing with class imbalance, with $\alpha$ being more felxible as it modifies the very shape of Shannon entropy's gradient curve, while $\lambda$ only scales it. While including both hyper-parameters would be interesting and would surely lead to better results, we wanted to keep the proposed formulation as simple and practically usable as possible, and only use one lever to deal with imbalance. 

## Miscallaneous clarifications

9- *Clarification for eq. (4).*

 The right-hand side of Eq. (4) is the definition of Tsallis $\alpha$-entropy. From the term in the middle in Eq. (4), one can recover the definition using the following steps: 

\begin{align}
\log_{\alpha}(K) - K^{1-\alpha} \mathcal{D}_{\alpha} ( \mathbf{p} || \mathbf{u}_K ) = \frac{1}{1-\alpha} \left( K^{1-\alpha}-1 \right) - \frac{K^{1-\alpha}}{\alpha-1} \left( \sum_k p_k^{\alpha} ( \frac{1}{K})^{1-\alpha} - 1 \right) 
 = \frac{1}{1 - \alpha} K^{1-\alpha} - \frac{1}{1 - \alpha}  - \frac{1}{\alpha-1} \sum_k p_k^{\alpha} + \frac{1}{\alpha-1}K^{1-\alpha} 
 = \frac{1 }{\alpha - 1} \left(1 - \sum_k p_k^{\alpha} \right) 
 = \mathcal{H}_\alpha ( \mathbf{p} )
\end{align}

The term $K^{1-\alpha}$ naturally disappears when $\alpha \rightarrow 1$, which is why it does not appear in the original Shannon Entropy in Eq (2). We will include this derivation in the final version of the paper.


10- *There is no performance for [15] in 10-shot and 20-shot settings with mini-ImageNet and tiered ImageNet*:

 In fact, we provided the performance of [15] in the 10-shot and 20-shot settings for the RN backbone (5th line in Table 1). For the WRN backbone, as mentioned at the end of the caption of Table 1, results of [15] were intractable to obtain within standard GPU hardware compute. Indeed, method [15] requires fine-tuning the whole network, which we found manageable for ResNet-18 memory-wise, but intractable for WRN and larger tasks. However, we do not expect the trend to be any different from the one observed on ResNet-18.


# R4

In what follows, figures and tables indexed with a letter (e.g Fig. A) can be found in the following anonymous link: https://github.com/anonymous6496/rebuttal , while figures indexed with a number are references to figures in the main paper.

## Choice of imbalance / additional imbalance scenarios

1- *Why is Dirichlet parameter a set to 2?*

We refer to answer 2- made to reviewer maGM.

2- *How does the performance change under different imbalance distributions?*

We refer to answer 1- made to reviewer maGM.

3- *Extremely, how does the method compare under a standard balanced scenario?*

We refer to answer 6- made to reviewer maGM.

## Choice of methods studied and reproduced

4- *Why is the paper focused only on transfer learning and not on meta-learning approaches? The current study is not comprehensive.*

In the popular transductive setting, which is the main focus of this study, we reported in Table 1 the 6 best-performing and most recent methods in the literature (all 6 from 2020 and 5 published in the top conferences), independently of  whether the methods are based on transfer learning or meta-learning. In fact, in Table 1, LR+ICI (CVPR’2020) and SIB (ICLR 2020) are meta-learning methods, whereas the other 4 are based on transfer learning. Also, we actually evaluated more meta-learning methods that use transductive batch normalization, including the very popular MAML (Finn et al., ICML 2017) and more recent transductive meta-learning methods that built on it like VERSA (ICML 2019); the results are in the Table below. We did not include the results of these methods in the main Table as they are not among the top-6 methods (their performances are significantly lower than the state-of-the-art). However, the conclusion is similar: these meta-learning methods, similarly to the more recent/competitive one (SIB and LR+ICI), are significantly affected by removing the artificial class balance. We will add the results of these methods in the supplemental material (as the main Table is already very big).


5- *The difference between inductive and transductive methods in this setting seems small and with stronger baselines claims might change.*

In fact, we report SimpleShot (also from end of 2019), which has a performance comparable to the three recent methods mentioned by the reviewer (MetaOptNet, CTM and DeepEMD). All inductive methods are still several points below the best-performing transductive methods, even in our new setting. For instance, in (miniImageNet, 1-shot, RN), MetaOptNet reports $62\%$, CTM $64\%$ and DeepEMD $65\%$, whereas Simpleshot in our Table 1 achieves $63\%$ with RN-18 and $66\%$ with WRN. The transductive methods achieve up to $70\%$.     

6- *The paper focuses on only two transductive methods  to show that the class-balance prior is encoded in these methods. What about other transductive methods?*

We mentioned that meta-learning and episodic training strategies build sequences of artificially balanced 
few-shot tasks (or episodes) during base training (lines 31-33). We also mentioned in several parts of the paper that carefully designed episodic schemes, which uses
strictly balanced support and query sets during meta-training, might encode implicitly class-balance biases (lines 59-63 and the beginning of section 4). In our experiments, as discussed in our answer above, we evaluated several recent and competitive meta-learning methods and observed significant drops in performances in the new setting. Therefore, as mentioned by the other reviewers, we believe our study is comprehensive in the context of transductive few-shot classification. We concede that the technical analysis of PT-MAP and TIM in Section 4 is longer that the discussions related to meta-learning methods. However, we beleive there are strong motivations for that. First, both were, at the time of submission, the two best performing transductive methods, which inevitably makes them relevant candidates. Second, each method utilizes popular regularization techniques in semi-supervised / unsupervised literature, namely mutual-information and optimal transport regularization, and we believe insights derived from analyzing these two methods will actually benefit researchers from a broader community than few-shot only.

As for BD-CSPN, the performance drops by noticeable margins too, although not at the same degree of severity as PT-MAP or TIM, as illustrated in the new 
Fig. A we provide, showing the performances of the top-5 transductive methods versus Dirichlet parameter $\boldsymbol{a}$.


## Hyperparameter tuning

7- *In Table 1, how is the $\alpha$ parameter tuned? Which values of $\alpha$ are reported in the table? Similarly for TIM, how is $\lambda$ tuned and which values are reported?*

As mentioned in lines. 261-264, we tune every hyper-parameter (including $\alpha$ and $\lambda$) using validation tasks with fixed Dirichlet parameter $a=1$, corresponding to uniformly random tasks. The range of values used to tune $\alpha$ on the validation tasks is the following goes from 1 to 10 by step of 1, while the range to validate $\lambda$ goes from 0 to 2, by step of 0.25. For each method, the best value obtained on validation tasks is then selected. The idea was to keep the hyperparameter budget similar, as mentioned in l.298.