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

---

## Switching the Claude Code Backend from Anthropic to Google Gemini

To swap out the backend provider from Anthropic to Google Gemini using either PowerShell or standard Command Prompt (CMD), you need to configure specific environment variables that tell the CLI tool to route requests to Google's API endpoint instead of Anthropic's.

Depending on which terminal interface you are currently using, choose the corresponding steps below.

### Option 1: Using PowerShell

Paste these commands directly into your PowerShell prompt. Replace `AIzaSyYourActualKeyHere` with your actual Gemini API key.

```powershell
# 1. Provide your Gemini API key
$env:GEMINI_API_KEY="AIzaSyYourActualKeyHere"

# 2. Redirect the tool's API URL to Google's OpenAI-compatible endpoint
$env:CLAUDE_CODE_API_URL="https://generativelanguage.googleapis.com/v1beta/openai/"

# 3. Specify the Gemini model you want to execute, for example gemini-2.5-pro or gemini-2.5-flash
$env:CLAUDE_CODE_MODEL="gemini-2.5-pro"

# 4. Start the application
claude
```

### Option 2: Using Command Prompt (CMD)

If you prefer standard Windows CMD, the syntax uses `set` instead of `$env:`. Paste these lines into your CMD window.

```cmd
:: 1. Provide your Gemini API key
set GEMINI_API_KEY=AIzaSyYourActualKeyHere

:: 2. Redirect the tool's API URL to Google's endpoint
set CLAUDE_CODE_API_URL=https://generativelanguage.googleapis.com/v1beta/openai/

:: 3. Specify the Gemini model
set CLAUDE_CODE_MODEL=gemini-2.5-pro

:: 4. Start the application
claude
```

### Why this works

Google's Gemini API exposes an OpenAI-compatible routing path at `/v1beta/openai/`. By telling the `claude` CLI tool to send its requests to that custom URL while passing your `GEMINI_API_KEY`, the tool routes requests to Google's models instead of the default Anthropic endpoint.

> Note: Environment variables set this way only last as long as that specific PowerShell or CMD window is open. If you close the terminal, you will need to paste those lines in again next time you launch it.

---

## Claude Code Backend von Anthropic zu Google Gemini wechseln

Um den Backend-Provider von Anthropic zu Google Gemini zu wechseln, kannst du entweder PowerShell oder die klassische Windows-Eingabeaufforderung (CMD) verwenden. Dafür setzt du bestimmte Environment Variables, damit das CLI-Tool Anfragen an Googles API-Endpunkt statt an Anthropic sendet.

Wähle je nach Terminal die passende Option.

### Option 1: PowerShell

Füge diese Befehle direkt in PowerShell ein. Ersetze `AIzaSyYourActualKeyHere` durch deinen echten Gemini API Key.

```powershell
# 1. Gemini API Key setzen
$env:GEMINI_API_KEY="AIzaSyYourActualKeyHere"

# 2. API-URL auf Googles OpenAI-kompatiblen Endpunkt umleiten
$env:CLAUDE_CODE_API_URL="https://generativelanguage.googleapis.com/v1beta/openai/"

# 3. Gemini-Modell auswählen, zum Beispiel gemini-2.5-pro oder gemini-2.5-flash
$env:CLAUDE_CODE_MODEL="gemini-2.5-pro"

# 4. Anwendung starten
claude
```

### Option 2: Command Prompt (CMD)

Wenn du die normale Windows-Eingabeaufforderung verwendest, nutzt du `set` statt `$env:`.

```cmd
:: 1. Gemini API Key setzen
set GEMINI_API_KEY=AIzaSyYourActualKeyHere

:: 2. API-URL auf Googles Endpunkt umleiten
set CLAUDE_CODE_API_URL=https://generativelanguage.googleapis.com/v1beta/openai/

:: 3. Gemini-Modell auswählen
set CLAUDE_CODE_MODEL=gemini-2.5-pro

:: 4. Anwendung starten
claude
```

### Warum das funktioniert

Die Gemini API von Google bietet einen OpenAI-kompatiblen Routing-Pfad unter `/v1beta/openai/`. Wenn du dem `claude` CLI-Tool diese benutzerdefinierte URL und deinen `GEMINI_API_KEY` gibst, werden die Anfragen an Googles Modelle statt an den Standard-Anthropic-Endpunkt gesendet.

> Hinweis: So gesetzte Environment Variables gelten nur für das aktuelle PowerShell- oder CMD-Fenster. Wenn du das Terminal schließt, musst du die Befehle beim nächsten Start erneut einfügen.

---

## تغییر Backend در Claude Code از Anthropic به Google Gemini

برای تغییر Backend Provider از Anthropic به Google Gemini می‌توانی از PowerShell یا Command Prompt معمولی ویندوز (CMD) استفاده کنی. باید چند Environment Variable تنظیم کنی تا ابزار CLI درخواست‌ها را به API گوگل بفرستد، نه به endpoint پیش‌فرض Anthropic.

بسته به ترمینالی که استفاده می‌کنی، یکی از گزینه‌های زیر را انتخاب کن.

### گزینه 1: استفاده از PowerShell

این دستورها را مستقیم داخل PowerShell قرار بده. مقدار `AIzaSyYourActualKeyHere` را با Gemini API Key واقعی خودت عوض کن.

```powershell
# 1. تنظیم Gemini API Key
$env:GEMINI_API_KEY="AIzaSyYourActualKeyHere"

# 2. تغییر API URL به endpoint سازگار با OpenAI در Google
$env:CLAUDE_CODE_API_URL="https://generativelanguage.googleapis.com/v1beta/openai/"

# 3. انتخاب مدل Gemini، مثلا gemini-2.5-pro یا gemini-2.5-flash
$env:CLAUDE_CODE_MODEL="gemini-2.5-pro"

# 4. اجرای برنامه
claude
```

### گزینه 2: استفاده از Command Prompt (CMD)

اگر از CMD معمولی ویندوز استفاده می‌کنی، به جای `$env:` باید از `set` استفاده کنی.

```cmd
:: 1. تنظیم Gemini API Key
set GEMINI_API_KEY=AIzaSyYourActualKeyHere

:: 2. تغییر API URL به endpoint گوگل
set CLAUDE_CODE_API_URL=https://generativelanguage.googleapis.com/v1beta/openai/

:: 3. انتخاب مدل Gemini
set CLAUDE_CODE_MODEL=gemini-2.5-pro

:: 4. اجرای برنامه
claude
```

### چرا این روش کار می‌کند

Gemini API گوگل یک مسیر سازگار با OpenAI در `/v1beta/openai/` ارائه می‌دهد. وقتی به ابزار CLI به نام `claude` این URL سفارشی و مقدار `GEMINI_API_KEY` را می‌دهی، درخواست‌ها به مدل‌های گوگل ارسال می‌شوند، نه به endpoint پیش‌فرض Anthropic.

> نکته: Environment Variable هایی که با این روش تنظیم می‌شوند فقط تا وقتی فعال هستند که همان پنجره PowerShell یا CMD باز باشد. اگر ترمینال را ببندی، دفعه بعد باید دوباره این دستورها را وارد کنی.
