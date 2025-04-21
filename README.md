# Customized Azure Document Extraction Tool

## Overview

The **Customized Azure Document Extraction Tool** enhances the default Azure Document Intelligence API, adding new capabilities for document extraction tasks. This tool is designed to handle large documents, resolve table issues, and extract data into a structured format like CSV and SQL.

## Features

### 1. **Extended Page Limit**
   - The default free-tier Azure Document Intelligence API has a limited page extraction capacity. This tool increases that limit, allowing the extraction of full-length documents and avoiding page constraints for multi-page PDFs.

### 2. **PDF Table Issues**
   - When tables are split across multiple pages in a PDF, the default tool often produces incomplete or inconsistent data. This tool resolves this by properly handling vertical cross-table data extraction, ensuring multi-page tables are fully captured.

### 3. **Dynamic Stitching Algorithm**
   - This tool uses a dynamic stitching algorithm to reassemble multi-page tables accurately, whether in scanned or native PDFs. The algorithm ensures that tables spanning across pages are reconstructed correctly, preserving the integrity of data.

### 4. **CSV and SQL Output**
   - After extracting tables from PDFs, the tool generates a CSV file for each table and converts the data into a SQL format. This makes it easy to store and process the extracted data in databases.

## Requirements

- **Azure Subscription**: An Azure account with access to the Azure Document Intelligence API.
- **Python 3.7+**: Python environment to run the tool and its dependencies.
- **pip**: Python package installer for managing required libraries.
- **SQL Database**: For storing extracted data (optional).

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/customized-azure-doc-extraction.git
   cd customized-azure-doc-extraction
   ```

2. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Setup

1. **Azure Credentials**:
   - Ensure that you have an Azure account with the Document Intelligence API enabled. 
   - Set up the required authentication (API keys or Azure Identity credentials) to interact with the Azure service.

2. **Configure the Tool**:
   - Modify the `config.json` file to include your Azure Document Intelligence API credentials and any necessary configuration details, such as custom endpoints.

3. **Environment Variables**:
   - Store your Azure API credentials in environment variables to keep them secure:
     ```bash
     export AZURE_DOCUMENT_INTELLIGENCE_KEY="your-api-key"
     export AZURE_DOCUMENT_INTELLIGENCE_ENDPOINT="your-endpoint-url"
     ```

## Project Structure

```
customized-azure-doc-extraction/
├── config.json              # Configuration file with Azure credentials and endpoints
├── extract_documents.py     # Main script for document extraction
├── requirements.txt         # Dependencies for the project
├── utils/                   # Utility scripts for processing extracted data
│   ├── csv_handler.py       # Handles conversion to CSV
│   └── sql_handler.py       # Handles conversion to SQL
├── data/                    # Directory for saving the extracted data
│   └── output/              # Output directory for extracted files
├── .env                     # Environment variables file
└── README.md                # Project documentation
```

## Usage

### Run the Extraction

1. To extract documents, use the following command:
   ```bash
   python extract_documents.py --input_file "path_to_your_document.pdf" --output_dir "path_to_output_directory"
   ```

2. **Features**:
   - The tool will extend the page limit for large documents.
   - It will resolve table issues and reconstruct multi-page tables.
   - For each table extracted, a CSV file will be generated, and the data will be converted into SQL.

### Example

Given an input document `example_document.pdf`, the tool will extract all pages, resolve table splits, and output the result into the directory `output/`. Each table will be stored in its own CSV file and converted into SQL.

```bash
python extract_documents.py --input_file "example_document.pdf" --output_dir "output/"
```

### Output Files

- **CSV Files**: A CSV file will be created for each table in the document, saved in the `output/` directory.
- **SQL Files**: The tables will be converted into SQL INSERT statements, suitable for database insertion.

## Additional Notes

- **CSV and SQL Output**: After extraction, the tool will create a separate CSV file for each table found in the document. These tables will then be converted into SQL scripts, which can be executed to insert the extracted data into a SQL database.
  
- **Data Integrity**: The dynamic stitching algorithm ensures that multi-page tables are accurately reconstructed, with no data loss across page breaks.

By using this tool, you can enhance your document processing workflows, ensuring accurate extraction and data storage for large or complex documents.
