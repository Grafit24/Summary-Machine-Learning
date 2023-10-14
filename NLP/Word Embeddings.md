---
tags:
  - NLP
  - embeddings
---
[NLP Course](https://lena-voita.github.io/nlp_course/word_embeddings.html)
## Введение
Что же такое word embeddings? Это векторна-числовая репрезентация [[Tokenization|токенов]] для модели.
![[Pasted image 20221017200744.png]]

## Vocabulary
На практике есть некоторый словарь доступных слов, которые вы выбираете заранее. В нём каждому слову из словаря соответсвует некоторый вектор - эмбединг, который находится по индексу слова в этом словаре.

Для слов которых нет в словаре, обычно, есть специальный токен UNK.
![[lookup_table.gif]]

## Как же получить эмбединг слова?

### One-hot вектора
Презентация $i$-го слова в словаре, как вектора с нулями везде кроме $i$-го элемента, который равен единицы. Сам вектор имеет размерность словаря.

**Недостатки**:
* Не понимает значения слов (стол=собака=кот);
* Дорого для памяти, ну камон целый словарь хранить для каждого слова.

### Distributional Semantics
Как понять значения слов? Люди понимают значения слов по их контексту, поэтому  ==слова которые часто встречаются в похожих контекстах -> имеют похожее значение==.

>**Главная идея:** ==нам нужно засунуть информацию о контексте слова в векторное представление==.

### Count-based methods
Эти методы решают задачу прямоленейно. 

>Count-based methods вносят информацию о контексте основываясь на global corpus statistics, то есть на глобальной статистике нашего корпуса текста.

![[Pasted image 20220515000420.png]]
Общий алгоритм этих методов:
1. Конструирование word-contex матрицы;
2. Уменьшаем её размерности.
	* для уменьшение занимаемой памяти;
	* для избавления от неинформативных контекстов, ведь слова появляются лишь в небольшом количестве контекстов. 

>dot product word/contex нормализированных векторов даёт близость/похожесть контекста к слову (или слова к контексту)

Для определния конкретного метода, требуется понять, что будет:
1. Possible contexts. Что вообще значит контекст? 
2. The notion of association - формула для расчёта элементов нашей матрицы.

#### Simple: Co-Occurence Counts
Самый простой способ определить **контекст** это взять окно размера L оцентровать его по слову и посчитать кажое слово встречающиесе в окне с центральным словом (**элемент матрицы**). И пройтись этим способом по всему тексту.
![[Pasted image 20221017204636.png]]
Элемент матрицы $(w, c)$ = $N(w, c)$ = это число раз, когда слово $c$ появилось в контексте (окне) слова $w$.
>[!Summarize]
>**Контекст**:
>Окружающие слова в окне размера L
>
> **Элемент матрицы:**
> $N(w, c)$ - количество раз, когда слово $c$ появилось в контексте (окне) слова $w$.

![[PPMI|Positive Pointwise Mutual Information (PPMI)]]

![[LSA|Latent Semantic Analysis (LSA)]]

![[Word2Vec]]

![[GLoVe]]

## Evaluation

![[Pasted image 20230909220120.png]]

![[Intrinsic Evaluation]]


![[Extrinsic Evaluation]]
## Interpretability
![[Pasted image 20230909220517.png]]

### How to get phrase embeddings (Simple method)
![[Pasted image 20230914135506.png]]

### Similarity across languages
![[Pasted image 20230909220759.png]]
$$W^*= \arg\min_W \sum_{i=1}^n||Wx_i - y_i||_2$$
$x_i$ - $i$ word embedding on first language.
$y_i$ - $i$ word embedding on second (target) language.
It can be shown that a self-consistent linear mapping between semantic spaces should be orthogonal.
We can restrict transform $W$ to be orthogonal. Then we will solve next problem:
$$W^*= \arg\min_W ||WX - Y||_F \text{, where: } W^TW = I$$
$$I \text{- identity matrix}$$
Instead of making yet another regression problem we can find optimal orthogonal transformation using singular value decomposition. It turns out that optimal transformation $W^*$ can be expressed via SVD components:
$$X^TY=U\Sigma V^T\text{, singular value decompostion}$$
$$W^*=UV^T$$