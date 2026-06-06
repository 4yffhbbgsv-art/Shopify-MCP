---
name: ai-image-generator
description: "Generate AI images using Gemini or GPT APIs directly."
---

# AI Image Generator

## Model Selection
- Photorealistic scenes → `gemini-3.1-flash-image-preview`
- Text on images / posters → `gpt-image-2`
- Transparent icons → `gpt-image-1.5`
- Quick drafts → `gemini-2.5-flash-image`

## Gemini (Python)

```python
python3 << 'PYEOF'
import json, base64, urllib.request, os, sys
GEMINI_API_KEY = os.environ.get("GEMINI_API_KEY")
if not GEMINI_API_KEY: print("Set GEMINI_API_KEY"); sys.exit(1)
model = "gemini-2.5-flash-image"
url = f"https://generativelanguage.googleapis.com/v1beta/models/{model}:generateContent?key={GEMINI_API_KEY}"
prompt = "PROMPT_HERE"
payload = json.dumps({"contents": [{"parts": [{"text": prompt}]}],"generationConfig": {"responseModalities": ["TEXT","IMAGE"],"temperature": 0.8}}).encode()
req = urllib.request.Request(url, data=payload, headers={"Content-Type": "application/json"})
resp = urllib.request.urlopen(req, timeout=120)
result = json.loads(resp.read())
for part in result["candidates"][0]["content"]["parts"]:
    if "inlineData" in part:
        img_data = base64.b64decode(part["inlineData"]["data"])
        with open("output.png","wb") as f: f.write(img_data)
        print(f"Saved output.png ({len(img_data):,} bytes)")
        break
PYEOF
```

## GPT Image 2 (text on images)

```python
python3 << 'PYEOF'
import json, base64, urllib.request, os
OPENAI_API_KEY = os.environ.get("OPENAI_API_KEY")
url = "https://api.openai.com/v1/images/generations"
payload = json.dumps({"model":"gpt-image-2","prompt":"PROMPT_HERE","n":1,"size":"1024x1024","quality":"medium","output_format":"png"}).encode()
req = urllib.request.Request(url, data=payload, headers={"Content-Type":"application/json","Authorization":f"Bearer {OPENAI_API_KEY}"})
resp = urllib.request.urlopen(req, timeout=180)
result = json.loads(resp.read())
img_data = base64.b64decode(result["data"][0]["b64_json"])
with open("output.png","wb") as f: f.write(img_data)
print(f"Saved output.png ({len(img_data):,} bytes)")
PYEOF
```

## 5-Part Prompt Framework
1. **Type**: "A photorealistic photograph"
2. **Subject**: who/what with specifics
3. **Environment**: setting and context
4. **Technical**: "Shot at 85mm f/2.0, natural window light"
5. **Constraints**: "No text, no watermarks, no logos"
