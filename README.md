# WeatherX API Integration Guide

## Introduction
WeatherX API allows developers to fetch **real-time weather data, 7-day forecasts, and weather alerts** for any city worldwide.  

**This tutorial covers:**  
- How to get your WeatherX API key  
- How to call endpoints using Postman  
- How to parse responses in Python or JavaScript  
- How to handle errors and common issues  

---

## Getting Started

### API Key
Sign up at [WeatherX.com](https://weatherx.com) and generate your API key from the developer dashboard.  
You will need this key to authenticate all API requests.

### Required Tools
- **Postman** (for testing API requests) — [Download](https://www.postman.com/downloads/)  
- **Code editor** (VS Code, Sublime, etc.)  
- **Python 3** or **Node.js/JavaScript** installed  

---

## Step-by-Step Integration

### Step 1 — Set Up Postman Request
1. Open Postman and create a new request.  
2. Enter the URL for the **Current Weather** endpoint:  
```
GET https://api.weatherx.com/v1/weather?city=Lagos
```  
3. Add the Authorization header:  
```
Authorization: Bearer YOUR_API_KEY
```  
4. Click **Send** and verify the response.

![Current Weather Request](assets/current-weather.png)

---

### Step 2 — Parse Response in Python
```python
import requests

url = "https://api.weatherx.com/v1/weather?city=Lagos"
headers = {"Authorization": "Bearer YOUR_API_KEY"}

response = requests.get(url, headers=headers)
data = response.json()

print(f"City: {data['city']}")
print(f"Temperature: {data['temperature']}°C")
print(f"Description: {data['description']}")
```

---

### Step 3 — Parse Response in JavaScript (Optional)
```javascript
const axios = require('axios');

const url = "https://api.weatherx.com/v1/weather?city=Lagos";
const headers = { Authorization: "Bearer YOUR_API_KEY" };

axios.get(url, { headers })
  .then(response => {
    const data = response.data;
    console.log(`City: ${data.city}`);
    console.log(`Temperature: ${data.temperature}°C`);
    console.log(`Description: ${data.description}`);
  })
  .catch(error => console.error(error.response.data));
```

---

### Step 4 — Fetch 7-Day Forecast
1. Use the endpoint:  
```
GET https://api.weatherx.com/v1/forecast?city=Lagos
```  
2. Add the Authorization header as before.  
3. Test in Postman.

![7-Day Forecast Request](assets/forecast.png)

4. Example Python snippet:
```python
url = "https://api.weatherx.com/v1/forecast?city=Lagos"
response = requests.get(url, headers=headers)
forecast = response.json()['forecast']

for day in forecast:
    print(f"{day['day']}: {day['temperature']}°C, {day['description']}")
```

---

### Step 5 — Fetch Weather Alerts
1. Endpoint:  
```
GET https://api.weatherx.com/v1/alerts?city=Lagos
```  
2. Add Authorization header.  
3. Test request in Postman.

![Weather Alerts Request](assets/alerts.png)

4. Example Python snippet:
```python
url = "https://api.weatherx.com/v1/alerts?city=Lagos"
response = requests.get(url, headers=headers)
alerts = response.json().get('alerts', [])

for alert in alerts:
    print(f"{alert['type']} — {alert['severity']}")
```

---

### Step 6 — Error Handling
```python
if response.status_code != 200:
    print("Error:", response.json().get('error', 'Unknown error'))
```

**Common errors:**  
- `401 Unauthorized` → Invalid API key  
- `404 Not Found` → Wrong city parameter  
- `429 Too Many Requests` → Rate limit exceeded  

---

## Tips & Best Practices
- Always handle errors gracefully  
- Respect API rate limits (60 requests per minute)  
- Test requests in Postman before integrating into your code  
- Store your API key securely  

---

## Conclusion
- You can now fetch **current weather, forecasts, and alerts** using WeatherX API  
- Next steps: integrate into a web or mobile app, explore other endpoints  

---

## Support
For assistance, contact:  
**support@weatherx.com**
