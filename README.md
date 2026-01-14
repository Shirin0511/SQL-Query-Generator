# 🧠 SQL Query Generator from Natural Language (NL → SQL)

This project implements a **schema-aware Natural Language to SQL (NL→SQL) system** by fine-tuning a pre-trained **T5 sequence-to-sequence model** on the **WikiSQL dataset**.

Given a **natural language question** and a **table schema**, the model generates a corresponding **SQL query**.  
The project focuses on **single-table SQL generation** and demonstrates an end-to-end **LLM fine-tuning and inference pipeline**.

---

## Project Highlights

- Fine-tuned **T5 (text-to-text transformer)** for NL→SQL generation
- Schema-aware prompting using column names and data types
- Supervised learning using WikiSQL structured annotations
- Lightweight SQL syntax validation (no execution)
- Clean separation of training, saving, and inference stages
- Designed with extensibility toward advanced datasets (Spider)

---

## Problem Statement

Translating natural language questions into SQL queries is a common requirement for data analysts and business users.  
This project explores how **large language models** can be fine-tuned to automate this translation when provided with **explicit schema context**.

---

## Model & Dataset

### Model
- **Base Model:** `t5-small`
- **Architecture:** Encoder–Decoder (Sequence-to-Sequence)
- **Training Strategy:** Supervised fine-tuning

### Dataset
- **WikiSQL**
  - Single-table SQL queries
  - Structured supervision for column selection, filtering, and aggregation
  - Designed for natural language question answering over tabular data

---

## 🏗️ System Architecture

