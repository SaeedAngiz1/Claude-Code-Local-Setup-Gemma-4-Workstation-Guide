# Using Gemini or Other Provider API Keys in Cloud Code with Python

This guide explains how to use a Gemini API key, or another provider API key, in Cloud Code with Python by storing the key in an environment variable instead of hardcoding it in your source code.

> Keep API keys out of your code files. Read them from environment variables at runtime.

---

## English

### 1. Set `GEMINI_API_KEY` in PowerShell for the current terminal session

This only applies to the current PowerShell window. If you close the terminal, the variable is gone.

```powershell
$env:GEMINI_API_KEY="your_gemini_api_key_here"
```

Verify that PowerShell can read it:

```powershell
echo $env:GEMINI_API_KEY
```

Run your Python script from the same PowerShell window:

```powershell
python app.py
```

### 2. Set `GEMINI_API_KEY` permanently for your Windows user account

This saves the variable for future PowerShell sessions.

```powershell
[Environment]::SetEnvironmentVariable("GEMINI_API_KEY", "your_gemini_api_key_here", "User")
```

Close and reopen PowerShell, then verify:

```powershell
echo $env:GEMINI_API_KEY
```

### 3. Use the environment variable in Python

```python
import os

gemini_api_key = os.getenv("GEMINI_API_KEY")

if not gemini_api_key:
    raise RuntimeError("GEMINI_API_KEY is not set. Set it in PowerShell before running this script.")

print("Gemini API key loaded successfully.")
```

### 4. Example Gemini Python request

Install the Google Gemini SDK:

```powershell
pip install google-genai
```

Create `app.py`:

```python
import os
from google import genai

api_key = os.getenv("GEMINI_API_KEY")

if not api_key:
    raise RuntimeError("GEMINI_API_KEY is not set.")

client = genai.Client(api_key=api_key)

response = client.models.generate_content(
    model="gemini-2.5-flash",
    contents="Explain environment variables in one short paragraph."
)

print(response.text)
```

Run it:

```powershell
python app.py
```

### 5. Use any other provider API key

The same pattern works for OpenAI, Anthropic, Groq, Mistral, OpenRouter, or any other provider.

PowerShell:

```powershell
$env:PROVIDER_API_KEY="your_provider_api_key_here"
```

Python:

```python
import os

provider_api_key = os.getenv("PROVIDER_API_KEY")

if not provider_api_key:
    raise RuntimeError("PROVIDER_API_KEY is not set.")

print("Provider API key loaded successfully.")
```

Recommended naming examples:

```powershell
$env:OPENAI_API_KEY="your_openai_api_key_here"
$env:ANTHROPIC_API_KEY="your_anthropic_api_key_here"
$env:GROQ_API_KEY="your_groq_api_key_here"
$env:OPENROUTER_API_KEY="your_openrouter_api_key_here"
```

---

## Deutsch

### 1. `GEMINI_API_KEY` in PowerShell nur für die aktuelle Sitzung setzen

Diese Methode gilt nur für das aktuelle PowerShell-Fenster. Wenn du das Terminal schließt, ist die Variable wieder weg.

```powershell
$env:GEMINI_API_KEY="dein_gemini_api_key_hier"
```

Prüfen, ob PowerShell den Key lesen kann:

```powershell
echo $env:GEMINI_API_KEY
```

Python-Skript im selben PowerShell-Fenster starten:

```powershell
python app.py
```

### 2. `GEMINI_API_KEY` dauerhaft für deinen Windows-Benutzer setzen

Diese Methode speichert die Variable für zukünftige PowerShell-Sitzungen.

```powershell
[Environment]::SetEnvironmentVariable("GEMINI_API_KEY", "dein_gemini_api_key_hier", "User")
```

PowerShell schließen, neu öffnen und prüfen:

```powershell
echo $env:GEMINI_API_KEY
```

### 3. Environment Variable in Python verwenden

```python
import os

gemini_api_key = os.getenv("GEMINI_API_KEY")

if not gemini_api_key:
    raise RuntimeError("GEMINI_API_KEY ist nicht gesetzt. Setze den Key zuerst in PowerShell.")

print("Gemini API Key wurde erfolgreich geladen.")
```

### 4. Beispiel für eine Gemini-Anfrage mit Python

Google Gemini SDK installieren:

```powershell
pip install google-genai
```

`app.py` erstellen:

```python
import os
from google import genai

api_key = os.getenv("GEMINI_API_KEY")

if not api_key:
    raise RuntimeError("GEMINI_API_KEY ist nicht gesetzt.")

client = genai.Client(api_key=api_key)

response = client.models.generate_content(
    model="gemini-2.5-flash",
    contents="Erkläre Environment Variables in einem kurzen Absatz."
)

print(response.text)
```

Ausführen:

```powershell
python app.py
```

### 5. Andere Provider-API-Keys verwenden

Dasselbe Muster funktioniert auch für OpenAI, Anthropic, Groq, Mistral, OpenRouter oder andere Anbieter.

PowerShell:

```powershell
$env:PROVIDER_API_KEY="dein_provider_api_key_hier"
```

Python:

```python
import os

provider_api_key = os.getenv("PROVIDER_API_KEY")

if not provider_api_key:
    raise RuntimeError("PROVIDER_API_KEY ist nicht gesetzt.")

print("Provider API Key wurde erfolgreich geladen.")
```

Empfohlene Namen:

```powershell
$env:OPENAI_API_KEY="dein_openai_api_key_hier"
$env:ANTHROPIC_API_KEY="dein_anthropic_api_key_hier"
$env:GROQ_API_KEY="dein_groq_api_key_hier"
$env:OPENROUTER_API_KEY="dein_openrouter_api_key_hier"
```

---

## فارسی

### 1. تنظیم `GEMINI_API_KEY` در PowerShell فقط برای همین نشست

این روش فقط برای همان پنجره PowerShell فعال است. اگر ترمینال را ببندی، متغیر حذف می‌شود.

```powershell
$env:GEMINI_API_KEY="کلید_gemini_خودت_اینجا"
```

بررسی کن که PowerShell بتواند کلید را بخواند:

```powershell
echo $env:GEMINI_API_KEY
```

اسکریپت Python را از همان پنجره PowerShell اجرا کن:

```powershell
python app.py
```

### 2. تنظیم دائمی `GEMINI_API_KEY` برای کاربر ویندوز

این روش متغیر را برای نشست‌های بعدی PowerShell ذخیره می‌کند.

```powershell
[Environment]::SetEnvironmentVariable("GEMINI_API_KEY", "کلید_gemini_خودت_اینجا", "User")
```

PowerShell را ببند، دوباره باز کن و بررسی کن:

```powershell
echo $env:GEMINI_API_KEY
```

### 3. استفاده از Environment Variable در Python

```python
import os

gemini_api_key = os.getenv("GEMINI_API_KEY")

if not gemini_api_key:
    raise RuntimeError("GEMINI_API_KEY تنظیم نشده است. قبل از اجرای اسکریپت آن را در PowerShell تنظیم کن.")

print("Gemini API key با موفقیت بارگذاری شد.")
```

### 4. نمونه درخواست Gemini با Python

نصب Google Gemini SDK:

```powershell
pip install google-genai
```

فایل `app.py` را بساز:

```python
import os
from google import genai

api_key = os.getenv("GEMINI_API_KEY")

if not api_key:
    raise RuntimeError("GEMINI_API_KEY تنظیم نشده است.")

client = genai.Client(api_key=api_key)

response = client.models.generate_content(
    model="gemini-2.5-flash",
    contents="Environment variables را در یک پاراگراف کوتاه توضیح بده."
)

print(response.text)
```

اجرا:

```powershell
python app.py
```

### 5. استفاده از کلید API برای هر Provider دیگر

همین الگو برای OpenAI، Anthropic، Groq، Mistral، OpenRouter یا هر سرویس‌دهنده دیگر هم کار می‌کند.

PowerShell:

```powershell
$env:PROVIDER_API_KEY="کلید_provider_خودت_اینجا"
```

Python:

```python
import os

provider_api_key = os.getenv("PROVIDER_API_KEY")

if not provider_api_key:
    raise RuntimeError("PROVIDER_API_KEY تنظیم نشده است.")

print("Provider API key با موفقیت بارگذاری شد.")
```

نام‌های پیشنهادی:

```powershell
$env:OPENAI_API_KEY="کلید_openai_خودت_اینجا"
$env:ANTHROPIC_API_KEY="کلید_anthropic_خودت_اینجا"
$env:GROQ_API_KEY="کلید_groq_خودت_اینجا"
$env:OPENROUTER_API_KEY="کلید_openrouter_خودت_اینجا"
```

