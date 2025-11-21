# Invoice Bounding Box Detection

Detect and visualize key sections of an invoice (Header, Line-Item Table, Totals) by drawing colored bounding boxes on top of the document.

This project takes an **invoice in PDF or Word format**, converts it into an image, uses **OpenCV** to detect text regions, and then classifies and highlights them using different colors.

---

## 1. Goals of the Project

- Load invoices in **PDF** or **Word (.docx, .doc)** format  
- Convert them into an image that OpenCV can process  
- Detect blocks of text (using thresholding, morphology & contours)  
- Categorize text regions into:
  - **Header section** (invoice metadata)
  - **Table section** (line items)
  - **Totals section** (summary, total amount, taxes, etc.)  
- Draw **colored bounding boxes**:
  - Header → **Blue**
  - Table → **Green**
  - Totals → **Red**
- Visualize results inside a **Jupyter Notebook** (and can be extended to Streamlit UI later)

---

## 2. Tech Stack

- **Language**: Python
- **Computer Vision**: OpenCV (`opencv-python`)
- **PDF to Image**: `pdf2image`
- **Word Document Handling**: `python-docx`
- **Image Processing & Arrays**: `numpy`
- **Plotting**: Matplotlib
- **UI (optional / future)**: Streamlit
- **Others**: `pillow` (PIL), `os`

---

## 3. Project Structure (Suggested)

You can organize the project like this:

```bash
invoice-bounding-box-detection/
│
├─ data/
│   ├─ sample_invoice.pdf
│   └─ sample_invoice.docx
│
├─ notebooks/
│   └─ invoice_bounding_box_demo.ipynb
│
├─ src/
│   ├─ loader.py          # load_invoice_as_image()
│   ├─ detection.py       # detect_text_blocks()
│   ├─ categorize.py      # categorize_blocks()
│   ├─ visualize.py       # draw_bounding_boxes()
│   └─ pipeline.py        # process_invoice()
│
├─ README.md
└─ requirements.txt

