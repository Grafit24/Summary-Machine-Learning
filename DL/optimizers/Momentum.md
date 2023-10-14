[Источник](https://ruder.io/optimizing-gradient-descent/)
#optimizer 

## Описание
![[momentum.png]]
Моментум — это метод, который позволяет ускорить SGD и погасить колебания. Методу удаётся это сделать за счёт добавления вектора обновления c предыдущего шага, умноженного на коэффициент $γ$.
$$v_t=γv_{t-1}+η∇_θJ(θ)$$
$$θ=θ−v_t$$
## Интуитивно
Моментум делает наш вектор градиент более похожем на мяч на который теперь действует сила притяжения, из-за чего он скатывается по сколону быстрее и быстрее. Бесконечно сохранять скорость ему не даёт сила сопротивления "воздуха" γ (сохраняемая энергия) при кажом степе. Когда же он перескакивает низ склона залетая на противоположный склон знак градиента меняется и скорость постепенно замедляется после чего, направление меняется и он катится снова к низу. Так он итеративно и доходит до минимума.