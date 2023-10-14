#adversarial-attacks, #CV
[Статья](https://arxiv.org/abs/1911.09665)
### Кратко
Обучение моделей с **adversarial examples** (aka данные с наложенным шумом) приводит к ухудшению результатов. Авторы выдвигают гипотезу о том, что это связано с тем что чистые изображения и adversarial из разных распределений, что приводит к тому, что [[Batch Normalization|batch norm]] (далее BN) учит что-то среднее между двумя этими распределниями, что в последствие приводит к деградация score'а.
![[Pasted image 20230203221115.png]]
Для решения этой проблемы предлагается использовать дополнительный BN (Auxiliary BN), который будет использоваться при прогоне батча из adversarial examples, при этом на этапе инференса отбрасывается и используется только основной.
![[Pasted image 20230203221518.png]]
При этом стоит заметить, что эту идею можно обобщить и использовать множество BNs для различных источников данных.

### Отсавшиеся вопросы
- Для меня не понятно, как мы используем Auxiliary BNs для генерации батча.
- PGD и как вообще создаются Adversial Examples

### Дальнейшее изучение
- [Pyramid Adversarial Training Improves ViT Performance](https://arxiv.org/abs/2111.15121)
- ⭐ [Towards Deep Learning Models Resistant to Adversarial Attacks](https://arxiv.org/pdf/1706.06083.pdf)
- [AutoAugument](https://arxiv.org/pdf/1805.09501.pdf)