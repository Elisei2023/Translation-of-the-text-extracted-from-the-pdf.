# Translation-of-the-text-extracted-from-the-pdf.
Translation of the text extracted from the pdf.

import os
from PyPDF2 import PdfReader
from tkinter import Tk
from tkinter.filedialog import askopenfilename
from deep_translator import GoogleTranslator  # Importă GoogleTranslator din deep_translator

"""Funcție pentru extragerea textului din PDF"""
def extract_text_from_pdf(pdf_path):
    text = ""
    reader = PdfReader(pdf_path)
    for page_num in range(len(reader.pages)):
        page = reader.pages[page_num]
        text += page.extract_text()
    return text

"""Funcție pentru traducerea textului în română"""
def translate_text_to_romanian(text):
    translated = GoogleTranslator(source='auto', target='ro').translate(text)
    return translated

"""Deschide o fereastră de selectare a fișierului PDF"""
def select_pdf_file():
    Tk().withdraw()  """Ascunde fereastra principală Tkinter"""
    pdf_path = askopenfilename(
        title="Selectează fișierul PDF",
        filetypes=[("PDF files", "*.pdf")]
    )
    if pdf_path:
        return pdf_path
    else:
        print("Nu a fost selectat niciun fișier.")
        return None

"""Selectarea fișierului PDF"""
pdf_path = select_pdf_file()

"""Extragerea textului dacă fișierul este selectat"""
if pdf_path and os.path.exists(pdf_path):
    print(f"Fișierul PDF selectat: {pdf_path}")
    extracted_text = extract_text_from_pdf(pdf_path)
    print("Text extras (primele 500 caractere):")
    print(extracted_text[:500])  """Afișează primele 500 de caractere din textul extras"""

  """"Traducerea textului în română"""
    translated_text = translate_text_to_romanian(extracted_text)
    print("\nText tradus în română:")
    print(translated_text[:500])
else:
    print("Fișierul nu a fost găsit sau nu a fost selectat.")
