# AJS Trading PRO — Render Deploy (Hindi)

## इस ZIP में क्या ठीक किया गया
- Project files को ZIP की root पर रखा है ताकि Render को `public/index.html` सही जगह मिले।
- `public/index.html` और `server.js` साथ में root में हैं; server static path `path.join(__dirname, "public")` इस्तेमाल करता है।
- `.env` और `node_modules` सुरक्षा/size के लिए ZIP में शामिल नहीं हैं।

## Render पर deploy
1. ZIP extract करें और अंदर के सभी project files को अपने GitHub repository के root में upload/commit करें। Repository में `server.js`, `package.json`, `public/index.html` सीधे root-level paths होने चाहिए — अतिरिक्त nested folder के अंदर नहीं।
2. Render Dashboard → Web Service → Settings में **Root Directory** खाली रखें यदि files repository root में हैं। अगर files किसी subfolder में हैं, Root Directory उसी subfolder पर set करें।
3. Build Command: `npm install`
4. Start Command: `npm start`
5. Environment tab में आवश्यक secrets set करें, जैसे `UPSTOX_ACCESS_TOKEN`। Token को GitHub या ZIP में न रखें। `REAL_TRADING_ENABLED` को `false` ही रखें जब तक real-order flow अलग से सुरक्षित रूप से validate न हो।
6. Manual Deploy → Clear build cache & deploy करें, फिर Logs देखें।

## अगर वही ENOENT error आए
Render के log में app path `/opt/render/project/src` हो तो इस path का मौजूद होना ज़रूरी है:
`/opt/render/project/src/public/index.html`
अगर नहीं है, GitHub repository की directory layout या Render Root Directory अभी भी गलत है।

Live market feed के लिए valid Upstox token, permissions और market session आवश्यक हैं। Deploy smoke test live market data की guarantee नहीं देता।
