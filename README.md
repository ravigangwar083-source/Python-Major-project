# Gen QrR 🔳

A Python-based QR code generator for website URLs and UPI payments, built with Flask, SQLite, and an interactive Jupyter Notebook dashboard.

## Features

- **Website QR Codes:** Convert HTTP and HTTPS URLs into QR codes.
- **UPI Payment QR Codes:** Generate QR codes using a UPI ID, payee name, optional amount, and payment note.
- **Instant Preview:** View generated QR codes inside Jupyter Notebook.
- **PNG Downloads:** Save QR codes as PNG images.
- **QR History:** Store and view previous QR codes using SQLite.
- **Delete Records:** Remove QR codes from history using their record IDs.
- **REST API:** Generate and manage QR codes through Flask endpoints.

## Tech Stack

| Technology | Purpose |
|---|---|
| Python | Core application logic |
| Flask | REST API |
| SQLite | QR history storage |
| qrcode | QR code generation |
| Pillow | Image processing |
| ipywidgets | Interactive notebook dashboard |
| Requests | Communication with the Flask API |

## Getting Started

### 1. Install Dependencies

Run the first cell of `Gen_QR.ipynb`, or install the packages manually:

```bash
pip install Flask "qrcode[pil]" Pillow requests ipywidgets
```

### 2. Open the Notebook

Open `Gen_QR.ipynb` in Jupyter Notebook using Anaconda or your preferred Python environment.

### 3. Run the Cells

Execute the notebook cells in order to initialize the database, start the Flask server, and display the dashboard.

The API runs locally at:

```text
http://127.0.0.1:5000
```

## How to Use

### Generate a Website QR Code

1. Select the URL option.
2. Enter a complete website URL beginning with `http://` or `https://`.
3. Add a label.
4. Click the generate button to preview and save the QR code.

### Generate a UPI QR Code

1. Select the UPI option.
2. Enter the UPI ID and payee details.
3. Add an amount and payment note if needed.
4. Click the generate button.

### Manage History

View saved records using the history button. To delete a record, enter its history ID and click the delete button.

## API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | View application information |
| GET | `/api/health` | Check server status |
| POST | `/api/qr/url` | Generate a website QR code |
| POST | `/api/qr/upi` | Generate a UPI QR code |
| GET | `/api/history` | Retrieve QR history |
| GET | `/api/qr/<id>/download` | Download a QR code as PNG |
| DELETE | `/api/history/<id>` | Delete a history record |

### Example: Generate a Website QR Code

```python
import requests

response = requests.post(
    "http://127.0.0.1:5000/api/qr/url",
    json={
        "url": "https://www.python.org",
        "label": "Python Website"
    },
    timeout=10
)

print(response.json())
```

### Example: Generate a UPI QR Code

```python
import requests

response = requests.post(
    "http://127.0.0.1:5000/api/qr/upi",
    json={
        "upi_id": "yourname@bank",
        "payee_name": "Your Name",
        "amount": "100",
        "note": "Sample payment"
    },
    timeout=10
)

print(response.json())
```

Replace the sample UPI details with your own before generating a payment QR code.

## Storage

The application creates the following folder in your user home directory:

```text
GEN_QR_Project/
├── qr_images/    # Generated PNG images
└── gen_qr.db     # SQLite database
```

## Payment Note

Generating a UPI QR code does not verify the UPI account or complete a payment. Check the recipient and amount in your payment app before confirming a transaction.

## Author

**Ravi Kumar**
