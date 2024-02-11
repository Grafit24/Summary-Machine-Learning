---
tags:
  - NLP
  - CV
  - compression
  - --draft
---
[Survey Arxiv](https://arxiv.org/pdf/2103.13630.pdf) [hf](https://huggingface.co/docs/optimum/concept_guides/quantization)
## Model Compression
**fp32** is too much precision (because of model robusty getted by for example [[Dropout]]) for model weights so we can compress model by half just convert weights to **fp16**. To train model in **fp16** is used [[Automatic Mixed Precision|AMP]] (mixed precision). To compress weights more is using quantization to **int8** (or smaller).

![[Pasted image 20240210005334.png]]

## Basic concepts of quantization
During quantization, the goal is to reduce the precision of both the weights $w_i$, as well as the intermediate activation maps (i.e., $h_i$ , $a_i$) to low-precision, with minimal impact on the generalization power/accuracy of the model.

We need first to define a function that can quantize NN weights and activations to a finite set of values.

**Uniform quantization**:
$$Q(r)=\operatorname{Int}(r/S)-Z$$
where
- $r$ is real valued **input** (activations or weights)
- $Z$ - is integer **zero point**
- $S$ - is real valued **scale factor**

>Note: There are also exists non-uniform quantization functions.

**Dequantization**:
$$\tilde{r}=S(Q(r)+Z)$$

### Calibration techniques
One important factor in uniform quantization is the choice of the scaling factor $S$. where $[α, β]$ denotes the **clipping range**, a bounded range that we are clipping the real values with, and b is the quantization bit width
$$S={\frac{\beta-\alpha}{2^{b}-1}}$$
The process of choosing the clipping range is often referred to as **calibration**.
#### Min/max calibration
**Asymmetric quantization**. $\alpha=r_{min}, \beta=r_{max}$.  It is called asymmetric, since the clipping range is not necessarily symmetric with respect to the origin, i.e. $-\alpha \neq \beta$. . It often results in a tighter clipping range. This is especially important when the target weights or activations are imbalanced, e.g., the activation after ReLU that always has non-negative values.
**Symmetric quantization**. $-\alpha\ =\ \beta\ =\ \mathrm{max}(|r_{m a x}|,|r_{m i n}|)$. $\alpha = -\beta$. Since quantization is symmetric we can use $Z=0$ that decreases computation.

>Note. As I understand asymetric/symmetric quantization may not necessarily be min/max

![[Pasted image 20240212000218.png]]

#### Percentile calibration
The clipping range is computed using a given percentile value $p$ on the observed values. The idea is to try to have $p$ of the observed values in the computed range. While this is possible when doing **assymetric quantization**.

![[Pasted image 20240210010736.png]]

#### [[KL Divergence]] calibration
Another approach is to select $α$ and $β$ to minimize KL divergence (i.e., information loss) between the real values and the quantized values.
- Entropy: the range is computed as the one minimizing the error between the full-precision and the quantized data.
- Mean Square Error: the range is computed as the one minimizing the mean square error between the full-precision and the quantized data.

### Range Calibration Algorithms
Another important differentiator of quantization methods is when the clipping range is determined. This range can be computed statically for weights, as in most cases the parameters are fixed during inference. However, the activation maps differ for each input sample.
- **Dynamic Quantization**, this range is dynamically calculated for each activation map during runtime. This approach requires real-time computation of the signal statistics (min, max, percentile, etc.) which can have a very high overhead. However, dynamic quantization often results in higher accuracy as the signal range is exactly calculated for each input.
- **Static quantization**: the range for each activation is computed in advance at _quantization-time_, typically by passing representative data through the model and recording the activation values.
- **Quantization aware training**: the range for each activation is computed at _training-time_, following the same idea than post training static quantization. But “fake quantize” operators are used instead of observers: they record values just as observers do, but they also simulate the error induced by quantization to let the model adapt to it.

### Quantization Granularity
- Layerwise/Tensorwise Quantization
- Groupwise Quantization. Transformers
- **Channelwise Quantization**
- Sub-channelwise Quantization


![[Pasted image 20240212001257.png]]

### Fine-tuning methods
- Quantization-Aware Training
- Post-Training Quantization

![[Pasted image 20240212003533.png]]


![[Pasted image 20240212003544.png]]

**Product Quantization**: Split vectors into chunks, quantize each chunk separately using K-means
**Orthogonal Product Quantization** First run #TODO **orthogonal transform**, then product quantization http://kaiminghe.com/publications/cvpr13opq.pdf 
**Additive Quantization** https://tinyurl.com/babenko-aq-pdf 
**Local Search Quantization** https://tinyurl.com/martinez-lsq-pdf