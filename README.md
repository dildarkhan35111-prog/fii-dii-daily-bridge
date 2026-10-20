# FII/DII Daily Bridge

यह bridge NSE के FII/FPI और DII cash-market data को रोज़ अपने-आप fetch करके JSON में रखता है।

## Flow

NSE
→ `fetch_fii_dii.py`
→ `data/latest.json`
→ GitHub Actions
→ रोज़ automatic update

## क्या मिलेगा

- FII Buy / Sell / Net
- DII Buy / Sell / Net
- FII score
- DII score
- Combined institutional net
- Institutional pressure
- FII/DII overview mark

## Important TradingView limitation

TradingView Pine Script arbitrary HTTPS APIs को सीधे call नहीं कर सकता।

TradingView का `request.seed()` custom GitHub EOD data पढ़ सकता है, लेकिन नए Pine Seeds repositories बनाना वर्तमान में suspended है। इसलिए यह bridge NSE data को automatic रूप से तैयार तो करेगा, लेकिन मौजूदा TradingView indicator में बिना किसी supported TradingView data-feed connection के JSON सीधे inject नहीं कर सकता।

अगर आपके पास पहले से कोई active Pine Seeds repository है, तो इस `data/latest.json` को उसके supported CSV feed में बदलकर `request.seed()` से जोड़ना अगला step होगा।

## Local test

```bash
pip install requests
python bridge/fetch_fii_dii.py
```

Output:
`data/latest.json`

## Cloud

GitHub Actions रोज़ 19:00 IST पर चलेगा। NSE data provisional होता है और बाद में revise हो सकता है।
