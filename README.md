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
## 4. Installation & Setup
## 4.1. Python Libraries

Install the required packages:
pip install opencv-python pdf2image python-docx pillow streamlit matplotlib

## 4.2. Poppler Installation (for PDF → Image)

pdf2image needs Poppler to convert PDF pages to images.

Download Poppler for Windows (e.g., from the official Poppler for Windows builds).

Extract it somewhere, e.g.:
C:\tools\poppler-25.11.0\Library\bin

This path will be used as poppler_path in the code.

Example in code:
poppler_path = r"poppler-25.11.0\Library\bin"
Adjust this path according to your actual poppler installation.

## 5. Core Functions
5.1. Load Invoice as Image
5.2. Detect Text Blocks (Contours + Morphology)
5.3. Categorize Blocks (Header / Table / Totals)
  This uses simple vertical position rules:
  
  Top 25% → Header
  
  Middle 50% → Table
  
  Bottom 25% → Totals
5.4. Draw Bounding Boxes
5.5. End-to-End Pipeline
## 6. Usage in Jupyter Notebook
Example notebook code to run the full pipeline and visualize

## 7. How the Algorithm Works (Conceptual)

Load Document

For PDFs: Convert first page to image using pdf2image.

For Word files: Extract text and draw it onto a blank white image.

Preprocess

Convert to grayscale.

Apply binary inverse threshold: text becomes white on black.

Morphological Operations

Use a rectangular kernel to connect nearby characters into larger blocks.

This helps treat each logical text block as one contour.

Contour Detection

cv2.findContours finds connected components in the dilated image.

Each contour is turned into a bounding rectangle.

Filtering Noise

Very small rectangles (height or width too small) are rejected.

Categorization

Based on the y-position of each box relative to image height.

Top → header, middle → table, bottom → totals.

Visualization

Draw colored rectangles on the original invoice image.

Display using Matplotlib.

## 8. Customization & Tuning

You can tweak the following to improve performance for different invoice layouts:

Thresholding

Adjust the value 180 in cv2.threshold.

Morphology Kernel

kernel = cv2.getStructuringElement(cv2.MORPH_RECT, (15, 3))

Increase width for connecting columns, increase height for connecting rows.

Noise Filtering

Change w > 40 and h > 20 rules in detect_text_blocks.

Section Boundaries

Adjust 0.25 and 0.75 thresholds in categorize_blocks.

## 9. Possible Extensions / Next Steps

Streamlit Web UI

Upload an invoice file via Streamlit.

Show side-by-side:

Original invoice

Invoice with bounding boxes.

Export Annotations

Save coordinates of detected header/table/totals as JSON or CSV.

OCR Integration

Combine with pytesseract to extract actual text from each block.

Multi-page PDFs

Loop through all pages of the PDF and process each page.

## 10. Known Limitations

Very noisy or low-resolution invoices may not segment well.

Complex layouts (multiple tables or side panels) may be misclassified.

The header/table/totals logic is purely positional (based on y-coordinate).






