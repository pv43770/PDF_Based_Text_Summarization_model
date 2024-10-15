PDF Summarization Using Fine-Tuned BART Model
This project fine-tunes the BART model (specifically facebook/bart-large-cnn) on text extracted from PDFs and generates summaries. The summaries are then stored in a MongoDB database.

Prerequisites
Ensure you have the following installed:

Python 3.7+
PyTorch
Hugging Face Transformers
MongoDB
SpaCy
PyPDF2
pdfplumber
pymongo
tqdm
To install the required Python libraries, run:

bash
Copy code
pip install torch transformers pymongo PyPDF2 pdfplumber spacy tqdm
Also, make sure you download the en_core_web_sm model for SpaCy:

bash
Copy code
python -m spacy download en_core_web_sm
Project Structure
graphql
Copy code
.
├── train_model.py                # Script for training and fine-tuning the BART model
├── summarize_pdfs.py             # Script for summarizing PDFs and storing summaries in MongoDB
├── fine_tuned_summary_model/     # Folder containing the fine-tuned BART model (generated after training)
├── fine_tuned_summary_tokenizer/ # Folder containing the tokenizer (generated after training)
└── README.md                     # This file
Workflow
1. Train and Save the Model
Use train_model.py to fine-tune the BART model on text extracted from PDFs and then save the model and tokenizer.

bash
Copy code
python train_model.py
What It Does:

Loads a folder of PDFs.
Extracts and preprocesses text.
Fine-tunes the BART model on the extracted text.
Saves the fine-tuned model and tokenizer to the specified path.
2. Summarize PDFs and Store in MongoDB
Use summarize_pdfs.py to generate summaries for PDFs and store them along with PDF metadata in a MongoDB collection.

bash
Copy code
python summarize_pdfs.py
What It Does:

Loads the fine-tuned BART model and tokenizer.
Extracts text and metadata from the PDFs.
Filters and chunks the text if necessary.
Generates summaries for each chunk using the fine-tuned model.
Stores the summaries and metadata in MongoDB.
3. Folder Structure for PDFs
Place your PDFs inside a folder. Ensure you set the correct path to your PDF folder in both train_model.py and summarize_pdfs.py:

python
Copy code
folder_path = r"C:\Users\pv437\Desktop\Data Scince Folder\Pankaj Assignments\Wasserstoff\Deployment\Jupyter Files\downloaded_pdfs"
Customization
PDF Preprocessing: You can modify the preprocessing function to clean your PDFs according to your requirements (for example, removing numbers, dates, etc.).
Model Tuning: You can experiment with the hyperparameters in train_model.py to adjust how the BART model learns from the data.
MongoDB Database
Database: pdf_summaries
Collection: summaries
Each summary stored in MongoDB will have the following structure:

json
Copy code
{
    "pdf_name": "example.pdf",
    "pdf_size_bytes": 123456,
    "pdf_pages": 10,
    "summary": "Generated summary text here..."
}
Saving & Loading the Model
Saving: The trained BART model and tokenizer are saved in the paths specified in the training script (train_model.py).
Loading: The model and tokenizer are loaded from the paths specified in the summarization script (summarize_pdfs.py).
Known Issues
Empty PDFs: If a PDF contains no extractable text, it will be skipped with a warning.
GPU Usage: The model will use GPU if available, otherwise it will fall back to CPU.
License
This project is licensed under the MIT License. You are free to modify and use it as needed.
