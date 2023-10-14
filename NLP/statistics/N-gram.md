[Источник](https://lena-voita.github.io/nlp_course/language_modeling.html#evaluation)
#NLP #language-modeling
## N-gram
Один из способов построение LM. Вычисляет вероятности используя [[Word Embeddings|global corpus statistics]], например просто считая кол-во вхождений в корпус текста.
**Марковское св-во**. Вероятность слова зависит только от фиксированного кол-ва предыдущих слов.
То есть для n-gram model:
$$P(y_t|y_1, ..., y_{t-1})=P(y_t|y_{t-n+1}, ..., y_{t-1})=\frac{N(y_1, y_2, ..., y_t)}{N(y_1, y_2, ..., y_{t-1})}$$
- $n=3$ - trigram model $P(y_t|y_{t-n+1}, ..., y_{t-1})=P(y_t|y_{t-2}, t_{t-1})$
- $n=2$ - bigram model $P(y_t|y_{t-n+1}, ..., y_{t-1})=P(y_t|t_{t-1})$
- $n=1$ - unigram model $P(y_t)$

### Решение проблемы 0 знаменателя
- **Backoff**. Использование меньшего контекста, когда больший неизвестен. То есть если знаменатель 0 при $n=4$ ("cat on a") мы используем $n=3$ ("cat on") и тогда далее до униграмной.
	- ![[Pasted image 20230311192941.png|300]]
- **Linear Interpolation**. $\sum \lambda_i = 1$. Это гиперпараметры которые мы подбираем с помощью [[Cross Validation]].
	- ![[Pasted image 20230311193003.png|300]]
- **Kneser-Ney**. Чтобы решить проблему Back-off в виде того что он может дать неоправданную частоту юниграме такой как San Francisco, где самого выражение встречается часто, но Francisco само по себе встречается редко.
	- ![[Pasted image 20230321210501.png|200]]
	- ![[Pasted image 20230321210707.png]]
	- [Подробнее](https://lena-voita.github.io/nlp_course/language_modeling.html#papers_smoothings)

### Решение проблемы 0 числителя
- **Laplace smoothing** (aka add-one smoothing). Притворимся, что мы видели все n-grams хотя бы $\delta$ раз. 
	- ![[Pasted image 20230311193539.png|300]]
- **Kneser-Ney Smoothing**.