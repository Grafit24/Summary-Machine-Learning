#metric #classification #object-detection 

**F-score** - это метрика представляющая из себя гармоническое среднее [[Precision]] и [[Recall]].
$$F_1=\frac{2}{\text{Precision}^{-1} + \text{Recall}^{-1}}=\frac{2 \cdot \text{Precision} \cdot \text{Recall}}{\text{Precision} + \text{Recall}}$$
Если $\beta > 1$, то вес [[Recall]] больше, если $\beta < 1$, то вес [[Precision]] больше. То есть чем больше $\beta$ тем больший вес даётся [[Recall]] и чем болье $1/\beta$ тем больший вес даётся [[Precision]].
$$F_{\beta}=(1+\beta^2)\frac{\text{Precision} \cdot \text{Recall}}{(\beta^2 \cdot \text{Recall}) + \text{Precision}}$$
> measures the effectiveness of retrieval with respect to a user who attaches β times as much importance to recall as precision.