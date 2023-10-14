#CV #generation #metric 
[Medium](https://medium.com/octavian-ai/a-simple-explanation-of-the-inception-score-372dff6a8c7a)
## Кратко
IS - это метрика, которая чем больше тем больше сгенерированное изображение похоже на реальное. Inception в название не просто так, ведь реальное распределение (как и сегенерированных изображений) берётся с помощью [[Inception]] модели. Другими словами оно будет ограничено датасетом на котором учился [[Inception]] и представленными в нём классами.
$$\text{IS}=exp(\mathbb{E}_x \{KL(p(y|x)\space||\space p(y))\})$$
KL - это [Kullback–Leibler divergence](https://en.wikipedia.org/wiki/Kullback–Leibler_divergence), это мера разности двух распределений $p(y|x)$ сгенерированного и реального $p(y)$б чем он больше тем больше эта разница.
$exp$ же нужна, чтобы разница между метриками была более выражена

В идеале сгенерированные изображения должны быть чётко разлчимы (определённый класс имеет наибольшую вероятность) и отличны от uniform distribution.
![[Pasted image 20230307165145.png]]

![[Pasted image 20230307165909.png]]

> Technically, we’re finding the _expectation value_, or average of the distributions, since we sum them and divide by the total count so the resulting distribution’s values sum to give 1.0