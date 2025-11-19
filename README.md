# OpenCV-Project
Invoice Bounding Box drawing 
• Take any invoice in pdf or word document 
• draw bounding box for key important fields and table using opencv , use different colours for different section

# Invoice Bounding Box Detection  
### PDF/DOCX → Image → OpenCV Layout Detection → Streamlit UI

This project processes invoice documents (PDF or Word) and automatically detects important regions using OpenCV, drawing color-coded bounding boxes around:

- **Header fields** (Vendor name, Invoice number, Date) — Blue  
- **Table/Line items** — Green  
- **Totals section** — Red  

The full pipeline works inside both **Jupyter Notebook** 

---

## 🚀 Features

✔ Converts PDF invoices to images using **Poppler**  
✔ Converts DOCX invoices to images using **python-docx**  
✔ Detects text blocks using **OpenCV morphological operations**  
✔ Categorizes blocks into header, table, totals  
✔ Draws **different colored bounding boxes**  
✔ Displays output in Jupyter Notebook  



