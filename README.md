# 👻 GhostTrader Chrome Extension 🔮

A passive chart analysis assistant powered by Google Gemini AI. This extension functions as a pure observer—no content scripts, no DOM injection, no bot detection risks.

## 📋 Features

✅ **Manifest V3 Compliant** - Modern, secure Chrome extension format  
✅ **Passive Observer Architecture** - All logic runs in the popup, zero DOM manipulation  
✅ **Gemini AI Integration** - Uses Gemini 1.5 Pro for advanced chart analysis  
✅ **No Build Tools Required** - Pure HTML, CSS, and Vanilla JavaScript  
✅ **Halloween Themed UI** - Spooky dark theme with glowing effects and atmospheric animations  
✅ **"Ghost of Wall Street" AI Persona** - Technical analysis delivered with spooky metaphors  
✅ **Local Storage** - API key saved securely in `chrome.storage.local`  
✅ **Error Handling** - Defensive coding with try-catch blocks throughout  

## 🚀 Installation

### Step 1: Get Your Gemini API Key

1. Go to [Google AI Studio](https://aistudio.google.com/apikey)
2. Click **"Create API Key"**
3. Copy your API key (keep it secret!)

### Step 2: Load the Extension in Chrome

1. Open Chrome and navigate to `chrome://extensions/`
2. Enable **"Developer mode"** (toggle in top-right corner)
3. Click **"Load unpacked"**
4. Select the `GhostTrader` folder containing:
   - `manifest.json`
   - `popup.html`
   - `popup.js`
   - `styles.css`

### Step 3: Use the Extension

1. Click the GhostTrader extension icon in your toolbar
2. Paste your Gemini API Key in the input field
3. Select your asset type (Real Pair or Synthetic)
4. Select the H1 major trend (Bullish, Bearish, or Ranging)
5. Navigate to any chart on your trading platform
6. Click **"SUMMON PREDICTION"** 👻🔮 - the extension will:
   - Capture a screenshot of the current tab
   - Send it to Gemini with your analysis rules
   - Display the recommendation: BET UP, BET DOWN, or NO TRADE

## 📁 File Structure

```
GhostTrader/
├── manifest.json      # Extension configuration (Manifest V3)
├── popup.html         # User interface markup
├── popup.js           # Core logic & API integration
├── styles.css         # Halloween theme styling
└── README.md          # This file
```

## 🎃 Halloween Theme

GhostTrader features a spooky Halloween aesthetic with:

- **Deep Purple/Black Gradient Backgrounds** - Atmospheric dark theme
- **Orange Fire Accents** (#ff6b00) - Glowing effects throughout
- **Floating Ghost & Crystal Ball Emojis** - Animated button decorations
- **Color-Coded Decisions** - Green (BET UP), Pink (BET DOWN), Orange (NO TRADE) with glow effects
- **Spooky Loading States** - "Summoning Spirits..." with orange gradient animation

### 👻 "Ghost of Wall Street" AI Persona

The AI analyst is a **100-year-old spirit trapped in the charts**, providing rigorous technical analysis with spooky metaphors:

**Bullish Signals**:
- "Rising from the grave"
- "The spirits are ascending"
- "Bulls rising from their graves"

**Bearish Signals**:
- "Descending into the abyss"
- "A bloodbath awaits"
- "Price being dragged down to hell"

**Uncertain/Ranging**:
- "Lost in the purgatory fog"
- "The fog is too thick"
- "The spirits are silent"

The AI maintains strict 4-step confluence analysis (trend, momentum, rejection, zones) but delivers insights through the lens of a supernatural market oracle.

## 🔐 Security Notes

- **API Key Storage**: Saved only in `chrome.storage.local` (device-only, never synced)
- **No Content Scripts**: Extension doesn't inject code into web pages
- **No DOM Manipulation**: Prevents bot/fraud detection triggers
- **API Calls**: Only to `generativelanguage.googleapis.com`
- **Screenshot**: Captured from your active tab locally, converted to base64, then sent to Gemini

## 🧠 How It Works

### Analysis Flow

```
User clicks "SUMMON PREDICTION" 👻🔮
    ↓
Captures visible tab as JPEG
    ↓
Converts to base64 format
    ↓
Constructs system prompt with user inputs
    ↓
Sends to Gemini 1.5 Pro with image + instructions
    ↓
Ghost of Wall Street analyzes chart structure, wicks, candles
    ↓
Returns JSON: { decision, confidence, reason }
    ↓
UI displays result with spooky color coding and glow effects
```

### System Prompt Rules

The extension includes hardcoded analysis rules:

1. **Real Pair + Ranging Trend** → Very conservative analysis
2. **Synthetic Assets** → Ignores external news context
3. **Visual Checks** → Looks for support/resistance structure (HH/HL/LH/LL) and rejection wicks
4. **Trap Detection** → Flags abnormally huge candles as potential traps (NO TRADE)

## 📊 Output Format

The extension displays:

- **Decision**: BET UP (glowing green), BET DOWN (glowing pink), NO TRADE (glowing orange)
- **Confidence**: Percentage (0-100%)
- **Reason**: One-sentence spooky explanation from the Ghost of Wall Street

Example:
```
Decision: BET UP
Confidence: 87%
Reason: The bulls are rising from their graves—rejection at the graveyard floor signals ascension
```

## 🛠️ Customization

### Modify Analysis Rules

Edit the `SYSTEM_PROMPT` in `popup.js`:

```javascript
const SYSTEM_PROMPT = `You are a strict Market Analyst.
INPUTS:
- Asset Type: [ASSET_TYPE]
- Major Trend: [MAJOR_TREND]
- Image: [The Screenshot]

RULES:
1. ... (add your custom rules here)

OUTPUT FORMAT (JSON ONLY): ...
```

### Add More Asset Types

In `popup.html`, add options to the Asset Type dropdown:

```html
<select id="assetType" class="select">
    <option value="Real Pair (EUR/USD)">Real Pair (EUR/USD)</option>
    <option value="Synthetic (Asia Composite)">Synthetic (Asia Composite)</option>
    <option value="Your Asset Here">Your Asset Here</option>
</select>
```

### Change UI Colors

The Halloween theme is defined in `styles.css`. Key color variables:

- Primary Accent: `#ff6b00` (orange fire)
- BET UP: `#00ff88` (bright green with glow)
- BET DOWN: `#ff3366` (hot pink with glow)
- NO TRADE: `#ffaa00` (orange with glow)
- Background: `#0a0a0a`, `#1a0a1a`, `#2a0a2a` (deep purple/black gradients)

## 🐛 Troubleshooting

| Issue | Solution |
|-------|----------|
| "Failed to capture chart image" | Ensure a browser tab is active when you click Analyze |
| "API Key is invalid" | Check your API key from [Google AI Studio](https://aistudio.google.com/apikey) |
| "API Error: 400 Bad Request" | Verify the image was captured and API key is correct |
| "No response from API" | Check your internet connection and API quota |
| Extension doesn't load | Ensure all 4 files are in the folder and manifest.json is valid JSON |

## 📜 API Endpoint

```
POST https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-pro:generateContent?key=YOUR_KEY

Payload:
{
  "contents": [{
    "parts": [
      { "text": "System prompt with analysis rules" },
      { "inline_data": { 
          "mime_type": "image/jpeg", 
          "data": "BASE64_ENCODED_IMAGE" 
        }
      }
    ]
  }]
}
```

## ⚡ Performance

- **Popup Opens**: ~100ms
- **Screenshot Capture**: ~500ms
- **API Response**: ~3-5 seconds (depends on Gemini processing)
- **Total Analysis Time**: ~4-6 seconds

## 📝 Version History

- **v1.0.0** (2025-11-19): Initial release
  - Manifest V3 support
  - Gemini 1.5 Pro integration
  - Halloween themed UI with glowing effects
  - "Ghost of Wall Street" AI persona
  - Local API key storage
  - System prompt with trading rules

## ⚠️ Disclaimer

This extension is a **passive analysis tool** and should not be used as financial advice. Always conduct your own research and use proper risk management. Past performance does not guarantee future results.

## 📄 License

This extension is provided as-is for educational and personal use.

---

**Need help?** Check the browser console (F12) for debug logs. All errors are logged to help troubleshoot issues.
