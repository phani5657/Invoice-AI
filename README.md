# AI Automated Invoice Processor

An AI-powered document processing system that automates invoice data extraction and invoice-to-PO verification. The system accepts invoice and purchase order documents, extracts structured information using an LLM, performs deterministic validation checks, and presents the results through a web interface.

## Overview

Processing invoices manually can involve reading documents, entering data, comparing invoices with purchase orders, and checking for inconsistencies.

This project automates that workflow by combining AI-based document extraction with rule-based validation.

The system can extract important invoice and purchase order fields, structure the information using Pydantic models, and compare the extracted data to identify mismatches and missing information.

## Key Features

- Upload invoice and purchase order documents through a web interface
- Extract structured information from documents using an LLM
- Extract fields such as:
  - Invoice number
  - Invoice date
  - Vendor name
  - Purchase order number
  - PO date
  - Line items
  - Quantities
  - Unit prices
  - Tax/GST details
  - Currency
  - Total amount
- Convert AI output into structured and validated data
- Compare invoice information with purchase order information
- Perform deterministic validation checks
- Identify missing or inconsistent information
- Detect amount and quantity discrepancies
- Check PO and invoice details such as currency and GST information
- Identify potential duplicate invoices
- Display extracted information and validation results through a simple frontend
- Process documents through a FastAPI backend

## Workflow

```text
Invoice / PO Upload
        ↓
Document Processing
        ↓
Text Extraction
        ↓
LLM-based Information Extraction
        ↓
Structured Pydantic Data
        ↓
Deterministic Validation
        ↓
Invoice vs PO Comparison
        ↓
Validation Results
        ↓
Web Interface
```

## How It Works

### 1. Document Upload

The user uploads an invoice and, when required, the corresponding purchase order through the web interface.

### 2. Text Extraction

The backend reads the uploaded documents and extracts their text so that the relevant information can be processed.

### 3. AI-based Extraction

The extracted document content is provided to an LLM with structured instructions to identify relevant invoice and purchase order fields.

Instead of returning unstructured text, the system converts the extracted information into structured objects.

### 4. Structured Validation

Pydantic models are used to validate the extracted data and ensure that the information follows the expected schema.

### 5. Deterministic Validation

Business rules are applied separately from the LLM.

The system can perform checks such as:

- Invoice and PO number matching
- Vendor information matching
- PO validity
- Quantity mismatches
- Unit price mismatches
- Total amount discrepancies
- Currency mismatches
- Missing GST information
- Duplicate invoice detection
- Missing required fields

This separation keeps business-critical validation deterministic instead of depending entirely on the LLM.

### 6. Results

The extracted information and validation results are returned by the FastAPI backend and displayed through the frontend.

## Architecture

```text
                ┌──────────────────┐
                │   Web Frontend   │
                └────────┬─────────┘
                         │
                         ▼
                ┌──────────────────┐
                │   FastAPI API    │
                └────────┬─────────┘
                         │
              ┌──────────┴──────────┐
              ▼                     ▼
       Document Processing      LLM Extraction
              │                     │
              └──────────┬──────────┘
                         ▼
                Structured Data
                         │
                         ▼
              Deterministic Checks
                         │
                         ▼
               Invoice / PO Results
```

## Tech Stack

### Backend

- Python
- FastAPI
- Pydantic
- Uvicorn

### AI

- Large Language Model (LLM)
- Prompt-based structured information extraction
- AI-assisted document understanding

### Document Processing

- PDF text extraction
- Document parsing

### Frontend

- HTML
- CSS
- JavaScript

### Development

- Git
- GitHub
- VS Code

## Project Structure

```text
Invoice-AI/
│
├── main.py
├── requirements.txt
├── .env
├── .gitignore
│
├── ...
│
└── README.md
```

The project structure may evolve as additional processing and validation modules are added.

## Running Locally

Clone the repository:

```bash
git clone https://github.com/Phanindrasadanala/Invoice-AI.git
cd Invoice-AI
```

Create a virtual environment:

```bash
python -m venv .venv
```

Activate the environment.

Windows:

```bash
.venv\Scripts\activate
```

Linux/macOS:

```bash
source .venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Create a `.env` file and add the required API keys/configuration.

Start the FastAPI server:

```bash
uvicorn main:app --reload
```

Open the application:

```text
http://127.0.0.1:8000
```

FastAPI API documentation is available at:

```text
http://127.0.0.1:8000/docs
```

## Example Use Case

A company receives an invoice from a vendor for a purchase order.

Instead of manually checking the invoice:

```text
Invoice
   ↓
Upload
   ↓
AI extracts invoice details
   ↓
PO details are extracted
   ↓
Invoice and PO are compared
   ↓
Validation checks are performed
   ↓
Mismatches are reported
```

For example, the system can identify situations such as:

```text
Invoice Amount:     ₹1,25,000
PO Amount:          ₹1,20,000
Difference:         ₹5,000
Status:             Amount mismatch
```

## Why AI + Deterministic Validation?

LLMs are useful for understanding unstructured documents because invoice formats can vary significantly between vendors.

However, business rules such as amount comparison, currency validation, duplicate detection, and PO verification should not depend only on an LLM.

Therefore, this project uses:

```text
LLM → Understand and extract information

Rules → Validate and compare information
```

This provides a more reliable approach for invoice processing.

## Future Improvements

- OCR support for scanned invoices
- Support for additional document formats
- Improved line-item matching
- More comprehensive invoice validation rules
- Database integration for invoice history
- Authentication and role-based access
- Batch invoice processing
- Human-in-the-loop approval workflow
- Improved duplicate detection
- Production deployment and monitoring

## Purpose

This project was built to explore how LLMs can be integrated into a real-world business workflow and combined with traditional backend engineering and deterministic business logic.

The main focus is on building a practical AI application rather than using an LLM as a standalone chatbot.
