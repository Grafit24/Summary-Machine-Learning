#NLP #tokenization
[NLP Course]()
## Byte pair encoding
BPE разбивает слова так, чтобы символы которые наиболее часто встречаются вместе, энкодились как один токен. Изначально это способ сжатия данных.

## Training
Учим BPE rules, какие пары символов объеденять. На этом этапе составляется merge table и tokens vocabulary. С самого начала словарь состоит из символов и пустого merge table, и изначально каждое слово делится на отдельные символы.

Алгоритм:
1. посчитать кол-во появлений пар символов
2. берётся наиболее частотная пара
3. эта пара добавляется как новый токен в словарь и в merge table
4. повторять пока не достигнется максимальное число объединений (на практике зависет от датасета, 4k-32k)

> In practice, the algorithm first counts how many times each word appeared in the data

> Note that after segmentation, we add the special characters **@@** to distinguish between tokens that represent entire words and tokens that represent parts of words.
![[build_merge_table.gif]]

## Inference
Применения выученных "BPE rules". В начале делим делим все слова на отдельные символы. Далее итеративно делаем следующие шаги:
1. из всех возможных мерджей из merge table, берём наиболее частотный
2. применяем этот мердж

![[bpe_apply.gif]]

**Fast implementations**:
- [YouTokenToMe](https://github.com/VKCOM/YouTokenToMe)
- [Sentencepiece](https://github.com/google/sentencepiece)