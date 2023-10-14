#NLP #prediction-based-method #count-based-method #embeddings 
## Идея
![[Pasted image 20230909213737.png]]

## Метод кратко
Схоже с [[Word2Vec]] мы имеет центральное слово и контекстные - наши параметры. Дополнительное мы добавляем scalar bias для кадого вектора.
Дополнительно метод контролирует влияние редко и часто встречающихся слов:
- rare events are penalized,
- very frequent events are not over-weighted.

![[Pasted image 20230909214121.png]]