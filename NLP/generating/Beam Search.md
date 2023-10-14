#NLP #seq2seq #-raw 
[NLP Course](https://lena-voita.github.io/nlp_course/seq2seq_and_attention.html)
## Beam Search
Параллельно генерируем beam_size ветвлений и на каждом этапе берём суммарно beam_size наиболее вероятных вариантов. В конце считаем произведение вероятностей кадого из получившихся последовательностей (веток) и выбираем наибольшее.  
![[beam_search.mp4]]

Обычно beam_size = 4 или 10.