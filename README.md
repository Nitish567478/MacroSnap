# 🥗 MacroSnap — AI Nutrition Buddy & WhatsApp Daily Tracker

> **Snap it. Track it. Text yourself the results.**  
> MacroSnap is an interactive AI-powered nutrition assistant built with **Streamlit**, **Google Gemini 2.5 Flash**, and **Twilio WhatsApp API**. It allows users to upload meal photos or type food descriptions, get instant calorie & macro breakdowns, and send an end-of-day nutritional summary straight to WhatsApp.

---

## 🚀 Features

- 📸 **Vision-Based Meal Analysis**: Upload photos (`jpg`, `jpeg`, `png`) of your meal to automatically estimate ingredients, calories, and macronutrients (protein, carbs, fat).
- 💬 **Interactive Chat Companion**: Conversational AI nutritionist that answers questions, adjusts estimates, and keeps conversations focused on health and fitness.
- 📲 **1-Click WhatsApp Summaries**: Generate an aggregated nutritional summary of all tracked meals throughout the session and deliver it directly to your WhatsApp via Twilio.
- ⚡ **Resilient AI Backend**: Equipped with automatic retry mechanisms and exponential backoff to handle transient API demand surges gracefully.
- 🔒 **Secure Secrets Management**: Built-in credential isolation using Streamlit secrets and `.gitignore`.

---

## 🛠️ Tech Stack

| Technology | Purpose |
| :--- | :--- |
| **Python 3.10+** | Core programming language |
| **[Streamlit](https://streamlit.io/)** | Web UI & conversational chat interface |
| **[Google GenAI SDK](https://ai.google.dev/)** (`gemini-2.5-flash`) | Multimodal vision & nutrition intelligence |
| **[Twilio REST API](https://www.twilio.com/)** | Automated WhatsApp message delivery |

---

## 📁 Project Structure

```text
workshope/
├── .streamlit/
│   ├── secrets.toml          # Private API keys & credentials (Git-ignored)
│   └── secrets.toml.example  # Public template for credentials
├── app.py                    # Main Streamlit application & Twilio integration
├── prompts.py                # AI system instructions and message templates
├── requirements.txt          # Python dependencies
├── .gitignore                # Git exclusions (credentials, venv, cache)
└── README.md                 # Project documentation
```

---

## ⚙️ Setup & Installation

### 1. Prerequisites
- Python 3.10 or higher installed
- A [Google AI Studio](https://aistudio.google.com/) API Key
- A [Twilio](https://www.twilio.com/) Account (with WhatsApp Sandbox or Business Sender)

---

### 2. Clone Repository & Setup Virtual Environment

```bash
# Clone the repository
git clone <your-repository-url>
cd workshope

# Create a virtual environment
python -m venv venv

# Activate the virtual environment
# On Windows:
venv\Scripts\activate
# On macOS / Linux:
source venv/bin/activate
```

---

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

### 4. Configure Secrets

Create a `.streamlit/secrets.toml` file in the project root:

```bash
mkdir .streamlit
```

Create/edit `.streamlit/secrets.toml` with your credentials:

```toml
GEMINI_API_KEY = "your-google-gemini-api-key"
TWILIO_ACCOUNT_SID = "your-twilio-account-sid"
TWILIO_AUTH_TOKEN = "your-twilio-auth-token"
TWILIO_WHATSAPP_FROM = "+14155238886"  # Twilio Sandbox number or your verified WhatsApp sender
TWILIO_CONTENT_SID = ""                # Optional: Leave empty for standard direct WhatsApp messages
```

> ⚠️ **Important:** Never commit `.streamlit/secrets.toml` to version control. It is already excluded in `.gitignore`.

---

### 5. Join Twilio WhatsApp Sandbox (Testing Mode)

If using the **Twilio Sandbox**:
1. Open your Twilio Console → **Messaging** → **Try WhatsApp**.
2. From your personal phone, send the prompt message (e.g., `join <your-sandbox-word>`) to the Twilio number (e.g., `+1 415 523 8886`).
3. You will receive a confirmation message that your phone number is connected.

---

## 🏃 Running the Application

Launch the Streamlit web app:

```bash
streamlit run app.py
```

The application will open in your browser at `http://localhost:8501`.

---

## 📖 How to Use

1. **Onboarding**:
   - Enter your name and WhatsApp number (with international country code, e.g. `+919876543210` or `+1234567890`).
   - Click **Let's go 🚀**.

2. **Track Meals**:
   - Type what you ate in the chat input, **OR**
   - Click the paperclip / file uploader icon to attach a photo of your meal.
   - The AI will provide meal breakdown, estimated calories, and macros (protein, carbs, fat).

3. **Send to WhatsApp**:
   - Click the **📤 Send to WhatsApp** button in the header.
   - A clean summary aggregating all meals and running daily totals will be sent to your WhatsApp inbox.

---

## 🛡️ Error Handling & Troubleshooting

- **503 UNAVAILABLE / High Demand Error**:  
  `app.py` automatically retries requests with exponential backoff if Google's Gemini servers experience transient spikes.
- **WhatsApp Message Fails to Deliver**:  
  - Ensure the destination phone number includes the country code (`+...`).
  - If using Twilio Sandbox, verify the recipient number has completed the `join <keyword>` handshake.
- **Twilio 400 Bad Request**:  
  If `TWILIO_CONTENT_SID` is blank, the app automatically switches to direct standard body messages.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
