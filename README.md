# Telugu Proverbs LoRA

LoRA fine-tune of Qwen2.5-0.5B-Instruct on a hand-built dataset of 30 Telugu proverbs. The model learns to answer a request with a Telugu proverb, its transliteration, an English translation, and a plain explanation of its meaning.

## What I built

- Dataset: 30 instruction/input/output examples (Alpaca format) in laya-proverbs-30.jsonl
- Training: Unsloth LoRA (r=16) on a free Colab T4 GPU - 60 steps, training loss 2.44 to 0.35
- Export: merged model converted to GGUF (Q8_0, ~519 MB) and run locally with Ollama as laya-tuned

## Run it yourself

1. Open telugu-proverbs-finetune.ipynb in Google Colab (GPU runtime) and run the cells in order.
2. The final cells export the GGUF file and a Modelfile. (The GGUF itself is not in this repo - at ~519 MB it exceeds GitHub's file-size limit.)
3. On your own machine, in the folder with the GGUF and Modelfile:
   ollama create laya-tuned -f Modelfile
   ollama run laya-tuned

## Sample

Ask: "Tell me a Telugu proverb about hard work and explain its meaning."
The model answers in the taught format: Telugu proverb, transliteration, translation, and meaning.

## Honest limitation

With only 30 examples, the model learns the answer format and style reliably, but the exact proverbs are sometimes blended or invented. Fine-tuning on a small dataset teaches behavior, not facts - more training data would improve factual accuracy. This mirrors the finding from my earlier RAG fine-tune (ragscope-lora).
