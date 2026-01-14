# 🧠 SQL Query Generator from Natural Language

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

## System Architecture

Natural Language Question
+
Table Schema
↓
Prompt Construction
↓
T5 Tokenizer
↓
Fine-tuned T5 Model
↓
SQL Query Output
↓
SQL Syntax Validation



---

## Input–Output Format

The model takes:
- **Schema**: column names with data types
- **Question**: natural language query

Example input:

```text
Schema: Name(text), Age(number), Salary(number), Department(text)
Question: What is the salary of Matthew?


Example Output:
SELECT Salary FROM table WHERE Name = 'Matthew'

## SQL Validation

The project includes **lightweight SQL syntax validation** using `sqlparse`.

- Ensures generated SQL is **syntactically parseable**
- Does **not execute queries**
- Keeps the system focused on **SQL generation**, not database interaction

```python
import sqlparse

def is_valid_sql(sql):
    return len(sqlparse.parse(sql)) > 0

---

## Running Inference

Use the fine-tuned model to generate SQL by providing a table schema and a natural language question.

schema = "Name(text), Age(number), Salary(number), Department(text)"
question = "What is the salary of Matthew?"

print(generate_sql(schema, question))


---


## Limitations

- Supports **single-table SQL only**
- No support for `GROUP BY`, joins, or nested queries
- Limited reliability for `AVG` due to dataset imbalance
- Weak semantic grounding for COUNT column selection
- No SQL execution or database integration

These limitations stem from **dataset constraints**, not implementation errors.

---

## Future Work

- Fine-tune on the **Spider dataset** to support:
  - Multi-table queries
  - `GROUP BY`
  - Joins and nested SQL
- Improve aggregation grounding
- Add an optional SQL execution layer
- Build an interactive UI using **Streamlit** or **Gradio**
