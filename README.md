# Tri-Media Steganography Platform 🔐

[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy?repo=https://github.com/nandu-dev-code/tri_media_stego)

A secure web application for concealing encrypted messages inside multimedia carrier files (**Images**, **Audio**, and **Video**) using authenticated cryptography and steganographic embedding with user authentication and QR + OTP verification.

---

## 🌟 Key Features

* **Multi-Carrier Steganography**:
  * **Images (PNG, JPG, BMP)**: Embeds QR code representation into RGB pixel least significant bits (LSB).
  * **Audio (16-bit PCM WAV)**: Encodes encrypted bits directly into audio sample LSBs.
  * **Video (MP4, AVI)**: Non-destructive overlay trailer steganography.
* **Military-Grade Cryptography**:
  * **AES-256-GCM** authenticated encryption with random salts and nonces.
  * **Scrypt KDF** (`N=16384, r=8, p=1`) protects passwords against GPU brute-force attacks.
* **Two-Factor Access Workflow (Image Stego)**:
  1. Sender embeds a secret message into an image cover.
  2. A unique access token is encoded into an embedded QR code, and ciphertext is securely persisted.
  3. Receiver extracts the QR code and requests a 5-minute single-use OTP.
  4. Scanning the QR code brings the user to the verification portal where OTP + Password decrypts the message.
* **Audit & Message History**:
  * Sender and receiver inboxes with tracking for `SENT`, `QR_EXTRACTED`, `DECRYPT_OK`, and `DECRYPT_FAIL`.

---

## 🚀 Local Quick Start

### 1. Clone & Set Up Virtual Environment

```bash
git clone https://github.com/nandu-dev-code/tri_media_stego.git
cd tri_media_stego

python -m venv venv
# Windows:
.\venv\Scripts\activate
# Linux/macOS:
source venv/bin/activate
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Configure Environment (Optional)

Copy `.env.example` to `.env`:
```bash
cp .env.example .env
```
* By default, the application runs with zero configuration using **SQLite** (`sqlite:///stegano.db`).
* To connect to **MySQL**, set `DATABASE_URL=mysql+pymysql://username:password@localhost/stegano_db`.
* To connect to **PostgreSQL**, set `DATABASE_URL=postgresql://username:password@host/dbname`.

### 4. Run the Application

```bash
python app.py
```
Open [http://127.0.0.1:5000](http://127.0.0.1:5000) in your browser.

---

## ☁️ Deployment

### Deploy to Render

1. Create a new account or log into [Render.com](https://render.com).
2. Click **New +** -> **Web Service**.
3. Select your repository: `nandu-dev-code/tri_media_stego`.
4. Configure the service:
   * **Runtime**: `Python`
   * **Build Command**: `pip install -r requirements.txt`
   * **Start Command**: `gunicorn app:app`
5. Click **Deploy Web Service**.

Alternatively, Render will automatically detect `render.yaml` and configure the service as a Blueprint.
