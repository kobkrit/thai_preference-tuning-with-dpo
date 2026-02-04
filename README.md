# Advanced Finetuning Strategy ภาษาไทย

บทเรียนการทำ Advanced Finetuning Strategy สำหรับ Large Language Models แปลและปรับปรุงเป็นภาษาไทย

เรียนรู้ทั้ง **SFT**, **DPO** และ **GRPO** พร้อมเปรียบเทียบผลลัพธ์:
1. **SFT (Supervised Fine-Tuning)** - สอนด้วยตัวอย่างที่ดี
2. **DPO (Direct Preference Optimization)** - สอนด้วยการเปรียบเทียบ
3. **GRPO (Group Relative Policy Optimization)** - สอนด้วย Reward Function

**ใช้ Qwen3-0.6B** - รองรับภาษาไทยและ Thinking Mode (`<think>` tags)

## เนื้อหาในโฟลเดอร์นี้

| ไฟล์ | Colab Link | คำอธิบาย |
|------|---------|---------|
| `00_create_preference_data_ollama.ipynb` | | สร้างข้อมูล Preference ด้วย Ollama (Local) |
| `00_create_preference_data_thaillm.ipynb` | [Colab](https://colab.research.google.com/drive/1drR8evzQY1IlmtoXxNo_I3eWGUMkpern?usp=sharing) | สร้างข้อมูล Preference ด้วย ThaiLLM API |
| `01_dpo_from_scratch_thai.ipynb` | [Colab](https://colab.research.google.com/drive/1fFIVthfOBHY0Fu287lqSUvuaY85-HpDE?usp=sharing) | **บทเรียนหลัก SFT vs DPO vs GRPO** ด้วย Qwen3-0.6B ⭐ |
| `dpo_thai_dataset.json` | | ข้อมูล DPO ภาษาไทย (100 รายการ) |
| `qwen3.py` | | Qwen3 Model Implementation |
| `images/` | | รูปภาพประกอบการสอน |

## ทำไมต้องใช้ Qwen3?

| Feature | Qwen3-0.6B |
|---------|------------|
| **ภาษาไทย** | ✅ รองรับ (100+ ภาษา) |
| **Thinking Mode** | ✅ มี (`<think>` tags) |
| **Parameters** | 600M (เหมาะกับการเรียนรู้) |
| **Context Length** | 32,768 tokens |
| **License** | Apache 2.0 (ใช้เชิงพาณิชย์ได้) |

## เปรียบเทียบเทคนิค

| หัวข้อ | SFT | DPO | GRPO |
|--------|-----|-----|------|
| **ข้อมูลที่ใช้** | คำตอบที่ดีเท่านั้น | คู่เปรียบเทียบ | Prompt + Verifier |
| **จำนวนโมเดล** | 1 | 2 | 1 |
| **Memory** | 1x | 2x | 1x + sampling |
| **เหมาะกับ** | Instruction Following | Preference Alignment | Math, Coding |

## Dataset

### DPO Dataset (Language Alignment)
```json
{
    "instruction": "อธิบายว่า Machine Learning คืออะไร",
    "chosen": "<think>ภาษาไทย...</think>\nMachine Learning คือ...",
    "rejected": "<think>English...</think>\nMachine Learning is..."
}
```

### GRPO Dataset (Thai Math)
```python
# คณิตศาสตร์เลขไทย (๐๑๒๓๔๕๖๗๘๙)
"๕ + ๓ = ?"  → "๘"
"๑๒ × ๔ = ?" → "๔๘"
```

## ลำดับการเรียน (3 ชั่วโมง)

### ชั่วโมงที่ 1: ทฤษฎีและข้อมูล
- SFT vs DPO vs GRPO คืออะไร? ต่างกันอย่างไร?
- รูปแบบข้อมูล Preference
- ทำไมต้องใช้ Qwen3?

### ชั่วโมงที่ 2: SFT & DPO Workshop
- โหลด Qwen3-0.6B
- สร้าง Dataset และ DataLoader
- ฝึกและทดสอบ SFT และ DPO Model

### ชั่วโมงที่ 3: GRPO Workshop และเปรียบเทียบ
- สร้าง Thai Math Dataset (เลขไทย)
- สร้าง Math Verifier
- ฝึกและทดสอบ GRPO Model
- เปรียบเทียบผลลัพธ์ทั้ง 3 เทคนิค

## ความต้องการของระบบ

```bash
pip install torch matplotlib tqdm safetensors huggingface_hub tokenizers
```

**Memory**: ~5 GB VRAM/RAM

## HuggingFace Dataset

[https://huggingface.co/datasets/iapp/dpo_thai_tutorial](https://huggingface.co/datasets/iapp/dpo_thai_tutorial)

**Dataset Creator:** Kobkrit Viriyayudhakorn (kobkrit@iapp.co.th), iApp Technology Co., Ltd.

## ผู้แปลและปรับปรุง

แปลและปรับปรุงโดย ดร.กอบกฤตย์ วิริยะยุทธกร (Kobkrit Viriyayudhakorn)
iApp Technology Co., Ltd.
kobkrit@iapp.co.th

## License

โค้ดต้นฉบับโดย Sebastian Raschka ภายใต้ Apache License 2.0

## อ้างอิง

> **Raschka, Sebastian. *Build A Large Language Model (From Scratch)*. Manning, 2024. ISBN: 978-1633437166.**

- หนังสือต้นฉบับ: [Build a Large Language Model From Scratch](http://mng.bz/orYv)
- Repository ต้นฉบับ: [https://github.com/rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch)
- Qwen3 Implementation: [rasbt/qwen3-from-scratch](https://huggingface.co/rasbt/qwen3-from-scratch)
- GRPO Paper: [DeepSeekMath: Pushing the Limits of Mathematical Reasoning](https://arxiv.org/abs/2402.03300)
