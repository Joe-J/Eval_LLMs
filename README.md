# Eval_LLMs
Compare the performances of the following LLMs

## Task
Using the benchmark below (lm-harness):
TinyLlama/EVAL.md at main · jzhang38/TinyLlama 

Compare the performances of the following LLMs (including the speed and memory):
- microsoft/phi-2 · Hugging Face
- TinyLlama/TinyLlama-1.1B-Chat-v1.0 · Hugging Face
- EleutherAI/pythia-1b · Hugging Face
- state-spaces/mamba 

## Installation
```python
# Install LM-Eval
!pip install git+https://github.com/EleutherAI/lm-evaluation-harness.git@big-refactor

# Download requirements of mamba 
!git clone https://github.com/state-spaces/mamba.git
!pip install causal-conv1d>=1.1.0
!pip install mamba-ssm
```

## Examples
```python
# mamba
!python /content/mamba/evals/lm_harness_eval.py --model mamba --model_args pretrained=state-spaces/mamba-130m --tasks hellaswag,openbookqa,winogrande,arc_easy,arc_challenge,boolq,piqa --device cuda:0 --batch_size 10 

# TinyLlama-1.1B-Chat-v0.1
!lm_eval \
    --model hf-auto \
    --model_args pretrained=PY007/TinyLlama-1.1B-Chat-v0.1,dtype="float" \
    --tasks hellaswag,openbookqa,winogrande,arc_easy,arc_challenge,boolq,piqa\
    --device cuda:0 --batch_size 10

# phi-2
!lm_eval \
    --model hf-auto \
    --model_args pretrained=microsoft/phi-2\
    --tasks hellaswag,openbookqa,winogrande,arc_easy,arc_challenge,boolq,piqa\
    --device cuda:0 --batch_size 10

# pythia-1b
!lm_eval \
    --model hf-auto \
    --model_args pretrained=EleutherAI/pythia-1b\
    --tasks hellaswag,openbookqa,winogrande,arc_easy,arc_challenge,boolq,piqa\
    --device cuda:0 --batch_size 10
```
## Performances
| Model                                         | HSwag | OBQA | WinoGrande | ARC_c | ARC_e | boolq | piqa | avg   |
|-----------------------------------------------|-------|------|---------|-------|-------|-------|------|-------|
| state-spaces/mamba-130m                | 35.30 | 28.60 | 52.41   | 42.05 | 24.23 | 55.14 | 63.33| 43.01 |
| microsoft/phi-2                     | 73.78 | 51.40 | 75.61   | 78.28 | 53.92 | 83.55 | 79.22| 70.82 |
| EleutherAI/pythia-1b                | 47.17 | 31.40 | 53.59   | 49.07 | 27.05 | 60.80 | 69.42| 48.36 |
| PY007/TinyLlama-1.1B-Chat-v0.1      | 53.81 | 32.20 | 55.01   | 49.62 | 28.67 | 58.04 | 69.64| 49.57 |


<!-- mamba (pretrained=state-spaces/mamba-130m), gen_kwargs: (), limit: None, num_fewshot: None, batch_size: 10
|    Tasks    |Version|Filter|n-shot| Metric |Value |   |Stderr|
|-------------|-------|------|-----:|--------|-----:|---|-----:|
|arc_challenge|Yaml   |none  |     0|acc     |0.1962|±  |0.0116|
|             |       |none  |     0|acc_norm|0.2423|±  |0.0125|
|arc_easy     |Yaml   |none  |     0|acc     |0.4798|±  |0.0103|
|             |       |none  |     0|acc_norm|0.4205|±  |0.0101|
|boolq        |Yaml   |none  |     0|acc     |0.5514|±  |0.0087|
|hellaswag    |Yaml   |none  |     0|acc     |0.3078|±  |0.0046|
|             |       |none  |     0|acc_norm|0.3530|±  |0.0048|
|openbookqa   |Yaml   |none  |     0|acc     |0.1680|±  |0.0167|
|             |       |none  |     0|acc_norm|0.2860|±  |0.0202|
|piqa         |Yaml   |none  |     0|acc     |0.6469|±  |0.0112|
|             |       |none  |     0|acc_norm|0.6333|±  |0.0112|
|winogrande   |Yaml   |none  |     0|acc     |0.5241|±  |0.0140|

hf-auto (pretrained=microsoft/phi-2), gen_kwargs: (), limit: None, num_fewshot: None, batch_size: 10
|    Tasks    |Version|Filter|n-shot| Metric |Value |   |Stderr|
|-------------|-------|------|-----:|--------|-----:|---|-----:|
|arc_challenge|Yaml   |none  |     0|acc     |0.5290|±  |0.0146|
|             |       |none  |     0|acc_norm|0.5392|±  |0.0146|
|arc_easy     |Yaml   |none  |     0|acc     |0.8001|±  |0.0082|
|             |       |none  |     0|acc_norm|0.7828|±  |0.0085|
|boolq        |Yaml   |none  |     0|acc     |0.8355|±  |0.0065|
|hellaswag    |Yaml   |none  |     0|acc     |0.5577|±  |0.0050|
|             |       |none  |     0|acc_norm|0.7378|±  |0.0044|
|openbookqa   |Yaml   |none  |     0|acc     |0.4040|±  |0.0220|
|             |       |none  |     0|acc_norm|0.5140|±  |0.0224|
|piqa         |Yaml   |none  |     0|acc     |0.7862|±  |0.0096|
|             |       |none  |     0|acc_norm|0.7922|±  |0.0095|
|winogrande   |Yaml   |none  |     0|acc     |0.7561|±  |0.0121|


hf-auto (pretrained=EleutherAI/pythia-1b), gen_kwargs: (), limit: None, num_fewshot: None, batch_size: 1
|    Tasks    |Version|Filter|n-shot| Metric |Value |   |Stderr|
|-------------|-------|------|-----:|--------|-----:|---|-----:|
|arc_challenge|Yaml   |none  |     0|acc     |0.2432|±  |0.0125|
|             |       |none  |     0|acc_norm|0.2705|±  |0.0130|
|arc_easy     |Yaml   |none  |     0|acc     |0.5703|±  |0.0102|
|             |       |none  |     0|acc_norm|0.4907|±  |0.0103|
|boolq        |Yaml   |none  |     0|acc     |0.6080|±  |0.0085|
|hellaswag    |Yaml   |none  |     0|acc     |0.3773|±  |0.0048|
|             |       |none  |     0|acc_norm|0.4717|±  |0.0050|
|openbookqa   |Yaml   |none  |     0|acc     |0.1860|±  |0.0174|
|             |       |none  |     0|acc_norm|0.3140|±  |0.0208|
|piqa         |Yaml   |none  |     0|acc     |0.7084|±  |0.0106|
|             |       |none  |     0|acc_norm|0.6942|±  |0.0107|
|winogrande   |Yaml   |none  |     0|acc     |0.5359|±  |0.0140|


hf-auto (pretrained=PY007/TinyLlama-1.1B-Chat-v0.1,dtype=float), gen_kwargs: (), limit: None, num_fewshot: None, batch_size: 10
|    Tasks    |Version|Filter|n-shot| Metric |Value |   |Stderr|
|-------------|-------|------|-----:|--------|-----:|---|-----:|
|arc_challenge|Yaml   |none  |     0|acc     |0.2560|±  |0.0128|
|             |       |none  |     0|acc_norm|0.2867|±  |0.0132|
|arc_easy     |Yaml   |none  |     0|acc     |0.5341|±  |0.0102|
|             |       |none  |     0|acc_norm|0.4962|±  |0.0103|
|boolq        |Yaml   |none  |     0|acc     |0.5804|±  |0.0086|
|hellaswag    |Yaml   |none  |     0|acc     |0.4206|±  |0.0049|
|             |       |none  |     0|acc_norm|0.5381|±  |0.0050|
|openbookqa   |Yaml   |none  |     0|acc     |0.2520|±  |0.0194|
|             |       |none  |     0|acc_norm|0.3220|±  |0.0209|
|piqa         |Yaml   |none  |     0|acc     |0.6959|±  |0.0107|
|             |       |none  |     0|acc_norm|0.6964|±  |0.0107|
|winogrande   |Yaml   |none  |     0|acc     |0.5501|±  |0.0140| -->
