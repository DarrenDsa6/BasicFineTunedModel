# Fine-Tuning TinyLlama for Text-to-SQL with LoRA

This project demonstrates how to fine-tune the **TinyLlama-1.1B-Chat-v1.0** model for the **Text-to-SQL** task using **LoRA (Low-Rank Adaptation)**.  

## 🔧 Environment Setup
- Installed essential libraries: `transformers`, `peft`, `accelerate`, `datasets`, `trl`, `sentencepiece`.  
- Verified Python, PyTorch, and CUDA environments for compatibility.  

## 📥 Base Model Loading
- Loaded **TinyLlama/TinyLlama-1.1B-Chat-v1.0** in FP16 precision.  
- Initialized tokenizer and displayed model parameters/memory footprint.  

## 🧪 Base Model Testing
- Implemented `build_prompt` to format Text-to-SQL prompts.  
- Tested on sample schema + question → results were verbose and incorrect SQL queries (baseline performance).  

## 📊 Dataset Preparation
- Used **b-mc2/sql-create-context** dataset.  
- Reduced to **3,500 samples** and split into training/evaluation sets.  
- Applied `format_example` to align examples with the chat template.  

## ⚡ LoRA Adaptors
- Attached LoRA adaptors with configuration:  
  - `r = 16`  
  - `lora_alpha = 32`  
  - `lora_dropout = 0.05`  
- Reduced trainable parameters significantly while enabling efficient fine-tuning.  

## 🎯 Model Fine-Tuning
- Fine-tuned for **1 epoch** using `SFTTrainer` from `trl`.  
- Training setup included:  
  - Gradient checkpointing  
  - Cosine learning rate scheduler  
  - AdamW optimizer  

## ✅ Post Fine-Tuning Results
- Evaluated on new schema-question probes.  
- Fine-tuned model generated **accurate, concise SQL queries**.  
- Demonstrated clear improvement over base model, validating the effectiveness of LoRA fine-tuning for Text-to-SQL.  

---

✨ In short: The project shows how **TinyLlama + LoRA** can achieve strong Text-to-SQL performance with minimal compute and memory overhead.
