# DPO (Direct Preference Optimization) ภาษาไทย

บทเรียนการทำ Direct Preference Optimization สำหรับ Large Language Models แปลและปรับปรุงเป็นภาษาไทย

**ใช้ Qwen3-0.6B** - รองรับภาษาไทยและ Thinking Mode (`<think>` tags)

## อ้างอิง

> **Raschka, Sebastian. *Build A Large Language Model (From Scratch)*. Manning, 2024. ISBN: 978-1633437166.**

- หนังสือต้นฉบับ: [Build a Large Language Model From Scratch](http://mng.bz/orYv)
- Repository ต้นฉบับ: [https://github.com/rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch)
- Qwen3 Implementation: [rasbt/qwen3-from-scratch](https://huggingface.co/rasbt/qwen3-from-scratch)

## เนื้อหาในโฟลเดอร์นี้

| ไฟล์ | คำอธิบาย |
|------|---------|
| `00_create_preference_data_ollama.ipynb` | สร้างข้อมูล Preference ด้วย Ollama (Local) |
| `00_create_preference_data_thaillm.ipynb` | สร้างข้อมูล Preference ด้วย ThaiLLM API |
| `01_dpo_from_scratch_thai.ipynb` | **บทเรียนหลัก DPO** ด้วย Qwen3-0.6B ⭐ |
| `dpo_thai_dataset.json` | ข้อมูล DPO ภาษาไทย (100 รายการ) |
| `qwen3.py` | Qwen3 Model Implementation |
| `images/` | รูปภาพประกอบการสอน |

## ทำไมต้องใช้ Qwen3?

| Feature | GPT-2 | Qwen3-0.6B |
|---------|-------|------------|
| **ภาษาไทย** | ❌ ไม่รองรับ | ✅ รองรับ (100+ ภาษา) |
| **Thinking Mode** | ❌ ไม่มี | ✅ มี (`<think>` tags) |
| **Parameters** | 124M | 600M |
| **Context Length** | 1,024 | 32,768 |

## Dataset

ข้อมูล DPO สำหรับสอนโมเดลให้ตอบเป็นภาษาไทย:

- **Chosen**: คำตอบ**ภาษาไทย** พร้อม `<think>` reasoning ✅
- **Rejected**: คำตอบ**ภาษาอังกฤษ** (ผิดภาษา!) ❌

```json
{
    "instruction": "อธิบายว่า Machine Learning คืออะไร",
    "input": "",
    "chosen": "<think>\nคำถามนี้ต้องการให้อธิบาย...\n</think>\n\nMachine Learning คือ...",
    "rejected": "<think>\nOkay, I need to explain...\n</think>\n\nMachine Learning is..."
}
```

## DPO คืออะไร?

**Direct Preference Optimization (DPO)** เป็นเทคนิคการฝึก LLM ให้ตอบสนองตามความชอบของมนุษย์

### ข้อควรรู้: ต้องโหลด 2 โมเดล!

```
Qwen3-0.6B:
- 1 โมเดล ≈ 1.2 GB (BF16)
- DPO (2 โมเดล) ≈ 2.4 GB + gradients ≈ 4-5 GB
```

## ลำดับการเรียน (3 ชั่วโมง)

### ชั่วโมงที่ 1: ทฤษฎีและข้อมูล
- DPO คืออะไร? เปรียบเทียบกับ RLHF
- รูปแบบข้อมูล Preference
- ทำไมต้องใช้ Qwen3?

### ชั่วโมงที่ 2: Workshop ปฏิบัติ
- โหลด Qwen3-0.6B
- สร้าง Dataset และ DataLoader
- คำนวณ DPO Loss

### ชั่วโมงที่ 3: Training และทดสอบ
- ฝึกโมเดลด้วย DPO
- Visualize ผลลัพธ์
- ทดสอบ Generation

## ความต้องการของระบบ

```bash
pip install torch matplotlib tqdm safetensors huggingface_hub tokenizers
```

**Memory**: ~5 GB VRAM/RAM สำหรับ Qwen3-0.6B DPO

## HuggingFace Dataset

[https://huggingface.co/datasets/iapp/dpo_thai_tutorial](https://huggingface.co/datasets/iapp/dpo_thai_tutorial)

**Dataset Creator:** Kobkrit Viriyayudhakorn (kobkrit@iapp.co.th), iApp Technology Co., Ltd.

## ผู้แปลและปรับปรุง

แปลและปรับปรุงโดย ดร.กอบกฤตย์ วิริยะยุทธกร (Kobkrit Viriyayudhakorn), iApp Technology Co., Ltd. สำหรับการอบรม NECTEC

## License

โค้ดต้นฉบับโดย Sebastian Raschka ภายใต้ Apache License 2.0
# thai_preference-tuning-with-dpo
