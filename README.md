## PDF OCR Extractor

Converts PDFs (text + images) into a TXT via OCR (Tesseract).

* **OCR language**: to add another language (e.g. English), install its Tesseract package in the Dockerfile (e.g. `tesseract-ocr-eng`) and set `lang="eng"` in `extract_pdf.py`. Default is Portuguese.
---

## Prerequisites

* **Docker** installed and running

  * Windows: follow [https://docs.docker.com/desktop/install/windows/](https://docs.docker.com/desktop/install/windows/)
  * macOS: follow [https://docs.docker.com/desktop/install/mac/](https://docs.docker.com/desktop/install/mac/)
  * Linux: follow [https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/)
* *(Optional, for local use)* **Python 3.7+**, **Tesseract OCR** and Python dependencies

---

## Usage

### Docker

1. **Clone the repository**

   ```bash
   git clone https://github.com/jofmatos/pdf-OCR-extractor.git
   cd pdf-OCR-extractor
   ```

2. **Verify Docker installation (optional)**

   ```bash
   docker --version
   ```

3. **Build the Docker image** (only once)

   ```bash
   docker build -t pdf-ocr-extractor .
   ```

4. **Run the container**

   * **Linux/macOS**

     ```bash
     docker run --rm \
       -v "$(pwd)":/app \
       pdf-ocr-extractor \
       your_file.pdf
     ```
   * **PowerShell (Windows)**

     ```powershell
     docker run --rm `
       -v "$($pwd.Path):/app" `
       pdf-ocr-extractor `
       your_file.pdf
     ```

   The script will process `your_file.pdf` and produce `your_file_ocr.txt` in the current directory.

---

### Local (no Docker)

1. **Create and activate a virtual environment**

   ```bash
   python -m venv .venv
   source .venv/bin/activate    # macOS/Linux
   .\.venv\Scripts\Activate.ps1 # PowerShell
   ```

2. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

3. **Run the script**

   ```bash
   python extract_pdf.py your_file.pdf
   ```

---

## Repository structure

```
pdf-ocr-extractor/
├── Dockerfile
├── .dockerignore
├── extract_pdf.py
├── requirements.txt
└── README.md
```

---

## Troubleshooting

* **Volume errors on Windows**: if you get permission or invalid-volume errors, try using an absolute host path or `${PWD}` in PowerShell.
* **Inspect container contents**: open an interactive shell inside the image:

  ```bash
  docker run --rm -it \
    -v "$(pwd)":/app \
    pdf-ocr-extractor \
    /bin/sh
  ```
