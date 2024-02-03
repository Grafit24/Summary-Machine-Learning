#NLP #CV
## What is LLM?
Модели имеющие >1b параметров и такие модели, которые от увелечения размера получают прирост качества.

LLMs:
- [[GPT|GPT 3/3.5/4]] - [OpenAI](https://openai.com/research/language-models-are-few-shot-learners)
- [[T5]] - [Arxiv](https://arxiv.org/abs/1910.10683)
- BLOOM
- [[BART]] - [Arxiv](https://arxiv.org/abs/1910.13461)

Является ли [[BERT]] LLM - ответ нет, поскольку она не получает достаточный прирост от увелечение размера. Задача заполения пропусков не является достаточно сложной.

## Parallelism
Операции:
- Scatter - отправь данные 
- Gather - возьми данные
- Broadcast - распространение данных на все ноды
![[Pasted image 20230417195222.png]]
- AllReduce operation is performing reductions on data (for example, sum, max) across devices and writing the result in the receive buffers of every rank.
![[Pasted image 20230417195111.png]]

**[[Data Parallel]]**:
- Одни и те же параметры на всех устройствах (в каждом девайсе по модели)
- После степа применяем AllReduce на параметры (или градиенты), усредняя их
- Тем самым мы получаем снова одинаковые модели после степа
- [Torch](https://pytorch.org/docs/stable/generated/torch.nn.DataParallel.html)

**[[Distributed Data Parallel]]**:
- Запускает не на тредах, а на процессах
- [Torch](https://pytorch.org/docs/stable/distributed.html)

![[Pasted image 20230417201155.png|300]]

**[[Pipelined Model Parallel]]**:
- Делим модель на части по слоям и храним эти части на каждом устройстве по отдельности
- Во время forward перекидывет выходы части с одной на вход другой
- Тоже самое во время backward
- [Arxiv](https://arxiv.org/abs/2104.04473)

![[Pasted image 20230417201700.png|300]]

**[[Tensor Model Parallel]]**:
- Разделение слоёв между девайсами
- [Arxiv](https://arxiv.org/abs/1909.08053)

![[Pasted image 20230417202909.png]]

![[Pasted image 20230417204000.png|500]]

**[[Sequence Model Parallel]]**:
- Разделение для [[Dropout]] и [[Layer Normalization]]
- [Arxiv](https://arxiv.org/abs/2205.05198)

**Gradients/parameters/optimizer [[Offloading]]**:
- Предлагается хранить на каждом девайсе только часть данных, а при их необходимости передавать их по быстрой шине.
- Также их можно хранить в RAM или SSD.
- Так хранение Optimizer States (в случае [[Adam]] это первые и вторые моменты в том числе) позволяет сократить расход памяти в 4 раза. Тоже самое можно проделать и с gradients и parameters. ![[Pasted image 20230417210443.png]]
- [Arxiv](https://arxiv.org/abs/1910.02054)

**Extreme case of distributed models**:
- Гомоскедастичность - распределённое обучение когда все устройства на которых мы обучаем модель одинаковы.
	- Например, мы обучаем на нашем сервере на нескольких tesla v100
- Гетероскедастичность - все устройства различны.
	- Например, мы обучаем модель на различных устройствах распределённых по миру связанных по интернету.
	- [Hivemind](https://github.com/learning-at-home/hivemind)

## Training Precision
Обычно fp32, что довольно много, поэтому можно сократить память с использованием fp16, но так как существует некоторые операции которым необходим fp32, то используется

**[[Automatic Mixed Precision]]**:
- Часть операций в fp32 часть в fp16
- Используем меньше памяти
- Быстрее на GPU
- ![[Pasted image 20230417213258.png]]
- [Torch](https://pytorch.org/docs/stable/amp.html)

Также можно использовать другой тип float: [bf16/tf16](https://blogs.nvidia.com/blog/2020/05/14/tensorfloat-32-precision-format/)
![[Pasted image 20230417214102.png|500]]

Quantization. 8 bit.
- LLM.int8 [Arxiv](https://arxiv.org/abs/2208.07339)
	- outliers значения (слишком большие) это наша проблема при квантизации 
	- ![[Pasted image 20230418203319.png]]
- SmoothQuant [GitHub](https://github.com/mit-han-lab/smoothquant)
	- ![[Pasted image 20230418203458.png]]

How to make your model faster:
- Cuda
- Triton
- FastTransformers for really fast inference

## PEFT: Parameter Efficient Fine-Tuning
- [[LayerNorm Adapters]]
- [[Soft Prompt|Soft Prompt tuning]]
- [[LoRA|Low Rank Adapters]]
- [[I3]]