#NLP #fine-tuning #LLM 
[Arxiv]()
## Low-rank adaptation of LLM
We hypothesize that the change in weights during model adaptation also has a low “intrinsic rank”
We hypothesize that the change in weights during model adaptation also has a low “intrinsic rank”

![[Pasted image 20230506205914.png]]

Advantages:
1. Одна предобученая модель может использоваться и создания мн-ва LoRA модулей для различных задач. Нам останется лишь менять матрицы A и B соответсвующие интересущей задачи.
2. LoRA много эффективнее при обучение и требует меньше ресурсов, ведь требуется только оптимизировать low-rank матрицы A и B.
3. Our simple linear design allows us to merge the trainable matrices with the frozen weights when deployed, introducing **no inference latency** compared to a fully fine-tuned model, by construction. (?)
4. LoRA is orthogonal to many prior methods and can be combined with many of them, such as prefix-tuning.



