---
tags:
  - NLP
  - domain-adaptation
---
## What is domain?
Domain - в контексте ML это некоторое многообразное подмножество данных имеющие общею специфику, например рецензии в интернете содержат в себе домейн  рецензий кинопоиска.

## Обозначения
- Model: $H=\{h_{\theta}:X\to Y\}$
- Data:
	- Source ~ training data : ${\mathcal{D}}_{S}=\{x_{i}^{S},y_{i}^{S}\}_{i=1}^{N}\sim P_{S}(x,y)$
	- Target ~ testing data : ${\mathcal{D}}_{T}=\{x_{i}^{T},y_{i}^{T}\}_{i=1}^{M}\sim P_{T}(x,y)$
- Task: $h_{\theta}^{\star}=\operatorname{arg\,min}R^{S}(h_{\theta})=\operatorname{arg\,min}_{(x,y)\sim P_{S}}[L(h_{\theta}(x),y)]$

## Domain Shift
Domain Shift означает что у насприсутвует смещение распределения target выборки из-за чего падает перфоманс модели, поэтому часто замеряют out-of-domain generalization.
$$P_{S}(x,y)\ne P_{T}(x,y)$$

Если распределения target и source отличаются, то мы можем натренировать бинарный классификатор чтобы их различить.  

### Generalization error under domain shift
Ben-David theory:
$$\epsilon_{T}\le\epsilon_{S}+\frac{1}{2}d_{H\Delta n}(D_{S},D_{T})+\lambda$$
- $\epsilon_{S}$ — expected source error
- $\frac{1}{2}d_{H\Delta n}(D_{S},D_{T})$ — the divergence between source and target domain
	- H-divergence measures the worst case of the disagreement between a pair of hypothesis. How much features discriminative for S and T
	- $d_{H\Delta H}(D_{S},D_{T})\sim d_{A}=2(1-2\varepsilon)$
- $\lambda=\operatorname*{min}_{h}[\epsilon_{S}(h)+\epsilon_{S}(h)]$ — error of ideal joint hypothesis

## Domain Adaptation
- Unsupervised - no labels for target domain
- Semi-supervised - target domain dataset is (partially) labeled

![[Pasted image 20240201224405.png]]

### [[Batch Normalization#Covariate Shift|Covariance Shift]]
$$P_{S}(x)\neq P_{T}(x)$$
$$P_{S}(y|x)=P_{T}(y|x)$$

## Instance weighting
Just add weight to samples from source with target distributions overlap
![[Pasted image 20240201224600.png]]

$$h_{\theta}^{\ast}=\arg\operatorname*{min}_{\theta}{\frac{1}{N}}\sum_{i=1}^{N}w(x_{i})L(h_{\theta}(x_{i}),y_{i})$$
$$w(x)={\frac{p r(x)}{p_{S}(x)}}$$

**Weighting using language models:**
$$w_{i}=\delta[H_{S}(x)-H_{T}(x)]$$
$$H=-\frac{1}{k}\log P(x)$$
$\delta$ - min-max regurilization

**Weighting using domain classifier:**
$$w_{i}=(1+p_{d}(x_{i}))$$
$p_{d}(x)$ - probability from being from target

## Data Selection
Instead of weighting, we can drop all observations that are too dissimilar from target domain.

![[Pasted image 20240201233227.png]]

![[Pasted image 20240201233302.png]]

Domain Similiarity Measures
![[Pasted image 20240201233340.png]]

## Proxy-labels methods
### Self-training
1. Train model on labeled data. 
2. Use confident predictions on unlabeled data as training examples. Repeat.
![[Pasted image 20240201233913.png]]

Ошибка усиливается т.к. модель не может исправить свою ошибку

### Tri-training
1. Train three models on bootstrapped samples. 
2. Use predictions on unlabeled data for third if two agree. 
3. Final prediction: majority voting

![[Pasted image 20240201234045.png]]

### Tri-training with disagreement
1. Train three models on bootstrapped samples. 
2. Use predictions on unlabeled data for third if two agree and prediction **differs**. (Добавляем только если две модели выдали одинаковые предсказания а третья отличающиеся от их предсказания) 
3. Final prediction: majority voting

### Asymmetric Tri-training
$\lambda|W_{1}^{T}W_{2}|$ - stimulate F1 and F2 to learn from different features

![[Pasted image 20240201234814.png]]

### Results
![[Pasted image 20240201235143.png]]

## Unsupervised in-domain pre-training
Due to the issue of catastrophic forgetting, the model may lose the information it has learned, even if the dataset includes a portion of our target domain. Therefore, after training the base model, it is necessary to perform unsupervised in-domain pre-training on the domain of interest to ensure the model retains relevant knowledge.

![[Pasted image 20240201235805.png]]

![[Pasted image 20240201235848.png]]

[[BERT|AdaptaBERT]]: 
1. Domain tuning: 50/50 source+target data unsupervised pretraining. 
2. Task tuning using source data

## Semi-supervised domain adaptation
![[Pasted image 20240202235733.png]]

## Distillation-like domain adaptation
1. Train teacher network 
2. Initialize student network by weights of teacher 
3. Train student with composite loss

![[Pasted image 20240203001712.png]]

$$L_{t o t a l}=(1-\lambda)L(q_{\theta})+\lambda D_{K L}(p\vert\vert q_{\theta})$$

## Domain adversarial neural networks
В этом подходе мы стремимся обучить нейронную сеть таким образом, чтобы фичи, извлекаемые из неё, минимизировали возможность определения, принадлежат ли данные исходному (source) или целевому (target) домену. Это делается с целью смягчить проблему забывания нейросетью данных source домена при обучении на данных target домена.

Example of #CV
• Train a classifier for the domain of an image based on deep convolutonal features.
• Try to maximize the loss of this classifier when training the CNN (confusion loss).
• Simultaneously, minimize the classification loss on the source domain using the same convolutional features.
• Train the digit classifier with source domain data, and the domain classifier with
domains's data.

![[Pasted image 20240203001903.png]]

DAAT = Domain-aware adversarial training 
1. Domain-distinguish task + target domain MLM 
2. Adversarial training