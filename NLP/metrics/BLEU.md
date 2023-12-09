---
tags:
  - NLP
  - metric
  - machine-translation
---
[Источник](https://en.wikipedia.org/wiki/BLEU)
## Кратко
Это алгоритм оценки машинного перевода между языками. В центре его идея о том, что чем ближе машинный перевод к переводу проффессионального переводчика тем лучше.

> Scores are calculated for individual translated segments—generally sentences—by comparing them with a set of good quality reference translations. Those scores are then averaged over the whole corpus to reach an estimate of the translation's overall quality. Intelligibility or grammatical correctness are not taken into account.

$$\text{BLEU} \in [0, 1]$$
Чем больше тем ближе машинный перевод к проффессиональному тексту.

## Math short
Here's the basic math behind it:
1. **N-gram precision**: First, it calculates precision for n-grams (groups of n words). For example, given the candidate sentence "the cat is on the mat" and reference sentence "the cat sat on the mat", the 1-gram precision is 5/6 because five out of six words in the candidate sentence are found in the reference sentence.
2. **Clipping**: However, this precision measure can be gamed by just repeating the most common words, so BLEU introduces a clipping mechanism. The count of each n-gram in the candidate sentence is clipped to the maximum number found in any reference sentence.
3. **Brevity Penalty (BP)**: To penalize short translations, BLEU uses a brevity penalty. If candidate translation length (c) is less than the reference sentence length (r), the BP is calculated as exp(1 - r/c). If c is greater than or equal to r, the BP is 1.

The final BLEU score is then the geometric mean of the n-gram precisions multiplied by the brevity penalty. In other words, for a candidate sentence with p1, p2, p3, p4 as the precision scores for 1-gram, 2-gram, 3-gram, and 4-gram respectively, the BLEU score is:

$$\text{BLEU} = \text{BP} \cdot \exp \left( \sum_{n=1}^{4}w_i \log(p_n) \right)$$
default $w_i=\frac{1}{4}$

The BLEU metric ranges from 0 to 1. The closer the score is to 1, the more the candidate translation matches the reference translations.

## Limitations
- BLEU сравнивает пересечение предсказанных токенов и референсов, вместо того чтобы сравнивать смысл. Это может привести к расхождениям между оценками BLEU и человеческой оценкой.
- Меньшие предсказания имеют более высокий score, чем длинные. Поэтому существует brevity penalty.
- BLEU scores не сопоставимы между разными датасетами и между различными языками.
- BLEU оценки могут сильно варьироваться в зависимости от того, какие параметры используются для генерации оценок, особенно при использовании различных методов токенизации и нормализации. 