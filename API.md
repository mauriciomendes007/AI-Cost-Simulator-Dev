# AI Cost Simulator - API Documentation

Complete API documentation for integrating AI Cost Simulator into your applications and AI bots.

## 📡 Base URL

```
https://ai-cost-simulator.com/api
```

**Status**: Currently in development. Web interface is fully functional. Backend API coming soon.

## 🔑 Authentication

Currently, no authentication is required for public endpoints.

Future versions may require:
- API keys for rate limiting
- OAuth 2.0 for enterprise users

## 📊 Endpoints

### 1. Calculate Cost

Calculate the cost for a given model and token count.

**Endpoint:**
```
POST /api/calculate
```

**Request Body:**
```json
{
  "modelId": "openai/gpt-4",
  "inputTokens": 500000,
  "outputTokens": 100000,
  "currency": "USD"
}
```

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `modelId` | string | Yes | Unique identifier for the model (e.g., "openai/gpt-4") |
| `inputTokens` | number | Yes | Number of input tokens (≥ 0) |
| `outputTokens` | number | Yes | Number of output tokens (≥ 0) |
| `currency` | string | No | Currency code (USD, EUR, GBP, JPY). Default: USD |

**Response (Success):**
```json
{
  "success": true,
  "data": {
    "inputCost": 0.075,
    "outputCost": 0.03,
    "totalCost": 0.105,
    "currency": "USD",
    "model": {
      "id": "openai/gpt-4",
      "name": "OpenAI GPT-4",
      "provider": "openai",
      "inputPrice": 0.00015,
      "outputPrice": 0.0003
    },
    "timestamp": "2026-09-12T08:45:00Z",
    "exchangeRate": 1.0
  }
}
```

**Response (Error):**
```json
{
  "success": false,
  "error": {
    "code": "INVALID_MODEL",
    "message": "Model not found: invalid-model-id",
    "details": "Ensure modelId is from the /models endpoint"
  }
}
```

**Example: JavaScript/Fetch**
```javascript
const response = await fetch('https://api.ai-cost-simulator.com/api/calculate', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    modelId: 'openai/gpt-4',
    inputTokens: 500000,
    outputTokens: 100000,
    currency: 'USD'
  })
});

const result = await response.json();

if (result.success) {
  console.log(`Total cost: ${result.data.currency}${result.data.totalCost}`);
  console.log(`Breakdown: Input ${result.data.currency}${result.data.inputCost} + Output ${result.data.currency}${result.data.outputCost}`);
} else {
  console.error(`Error: ${result.error.message}`);
}
```

**Example: Python/Requests**
```python
import requests
import json

url = 'https://api.ai-cost-simulator.com/api/calculate'
payload = {
    'modelId': 'openai/gpt-4',
    'inputTokens': 500000,
    'outputTokens': 100000,
    'currency': 'USD'
}

response = requests.post(url, json=payload)
result = response.json()

if result['success']:
    data = result['data']
    print(f"Total cost: {data['currency']}{data['totalCost']}")
    print(f"Input cost: {data['currency']}{data['inputCost']}")
    print(f"Output cost: {data['currency']}{data['outputCost']}")
else:
    print(f"Error: {result['error']['message']}")
```

**Example: cURL**
```bash
curl -X POST https://api.ai-cost-simulator.com/api/calculate \
  -H "Content-Type: application/json" \
  -d '{
    "modelId": "openai/gpt-4",
    "inputTokens": 500000,
    "outputTokens": 100000,
    "currency": "USD"
  }'
```

**Example: Node.js/Axios**
```javascript
const axios = require('axios');

async function calculateCost() {
  try {
    const response = await axios.post(
      'https://api.ai-cost-simulator.com/api/calculate',
      {
        modelId: 'openai/gpt-4',
        inputTokens: 500000,
        outputTokens: 100000,
        currency: 'USD'
      }
    );

    const data = response.data.data;
    console.log(`Total: ${data.currency}${data.totalCost}`);
  } catch (error) {
    console.error('API Error:', error.response.data.error);
  }
}

calculateCost();
```

---

### 2. Get All Models

Retrieve all available models with pricing information.

**Endpoint:**
```
GET /api/models
```

**Query Parameters:**

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `provider` | string | - | Filter by provider (openai, anthropic, google, etc.) |
| `limit` | number | 100 | Maximum results to return (1-1000) |
| `offset` | number | 0 | Pagination offset |
| `sort` | string | name | Sort by: name, inputPrice, outputPrice |

**Response (Success):**
```json
{
  "success": true,
  "data": [
    {
      "id": "openai/gpt-4",
      "name": "OpenAI GPT-4",
      "provider": "openai",
      "inputPrice": 0.00015,
      "outputPrice": 0.0003,
      "currency": "USD",
      "lastUpdated": "2026-09-12T08:00:00Z"
    },
    {
      "id": "anthropic/claude-3-opus",
      "name": "Anthropic Claude 3 Opus",
      "provider": "anthropic",
      "inputPrice": 0.000015,
      "outputPrice": 0.000075,
      "currency": "USD",
      "lastUpdated": "2026-09-12T08:00:00Z"
    },
    {
      "id": "google/gemini-pro",
      "name": "Google Gemini Pro",
      "provider": "google",
      "inputPrice": 0.0000005,
      "outputPrice": 0.0000015,
      "currency": "USD",
      "lastUpdated": "2026-09-12T08:00:00Z"
    }
  ],
  "pagination": {
    "total": 150,
    "limit": 100,
    "offset": 0,
    "hasMore": true
  }
}
```

**Example: JavaScript/Fetch**
```javascript
// Get all models
async function getAllModels() {
  const response = await fetch('https://api.ai-cost-simulator.com/api/models');
  const result = await response.json();
  
  if (result.success) {
    console.log(`Found ${result.pagination.total} models`);
    result.data.forEach(model => {
      console.log(`${model.name}: $${model.inputPrice} / 1k input tokens`);
    });
  }
}

// Get models from specific provider
async function getOpenAIModels() {
  const response = await fetch(
    'https://api.ai-cost-simulator.com/api/models?provider=openai'
  );
  const result = await response.json();
  return result.data;
}

getAllModels();
```

**Example: Python**
```python
import requests

# Get all models
response = requests.get('https://api.ai-cost-simulator.com/api/models')
result = response.json()

if result['success']:
    for model in result['data']:
        print(f"{model['name']}: ${model['inputPrice']}")

# Get specific provider
response = requests.get(
    'https://api.ai-cost-simulator.com/api/models',
    params={'provider': 'anthropic'}
)
```

---

### 3. Get Model Details

Get detailed information about a specific model.

**Endpoint:**
```
GET /api/models/{modelId}
```

**Path Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| `modelId` | string | Model identifier (e.g., "openai/gpt-4") |

**Response (Success):**
```json
{
  "success": true,
  "data": {
    "id": "openai/gpt-4",
    "name": "OpenAI GPT-4",
    "provider": "openai",
    "description": "Most capable model from OpenAI",
    "contextWindow": 8192,
    "inputPrice": 0.00015,
    "outputPrice": 0.0003,
    "currency": "USD",
    "lastUpdated": "2026-09-12T08:00:00Z",
    "status": "active",
    "features": {
      "vision": false,
      "functionCalling": true,
      "streaming": true
    }
  }
}
```

**Example: JavaScript**
```javascript
async function getModelDetails(modelId) {
  const response = await fetch(
    `https://api.ai-cost-simulator.com/api/models/${modelId}`
  );
  const result = await response.json();
  
  if (result.success) {
    const model = result.data;
    console.log(`Model: ${model.name}`);
    console.log(`Context: ${model.contextWindow} tokens`);
    console.log(`Input: $${model.inputPrice} / 1k tokens`);
    console.log(`Output: $${model.outputPrice} / 1k tokens`);
  }
}

getModelDetails('openai/gpt-4');
```

---

### 4. Batch Calculate

Calculate costs for multiple models in one request.

**Endpoint:**
```
POST /api/batch-calculate
```

**Request Body:**
```json
{
  "calculations": [
    {
      "modelId": "openai/gpt-4",
      "inputTokens": 500000,
      "outputTokens": 100000
    },
    {
      "modelId": "anthropic/claude-3-opus",
      "inputTokens": 500000,
      "outputTokens": 100000
    }
  ],
  "currency": "USD"
}
```

**Response (Success):**
```json
{
  "success": true,
  "data": [
    {
      "modelId": "openai/gpt-4",
      "modelName": "OpenAI GPT-4",
      "totalCost": 0.105,
      "inputCost": 0.075,
      "outputCost": 0.03
    },
    {
      "modelId": "anthropic/claude-3-opus",
      "modelName": "Anthropic Claude 3 Opus",
      "totalCost": 0.0125,
      "inputCost": 0.0075,
      "outputCost": 0.005
    }
  ],
  "currency": "USD"
}
```

**Example: JavaScript**
```javascript
async function compareCosts() {
  const response = await fetch(
    'https://api.ai-cost-simulator.com/api/batch-calculate',
    {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        calculations: [
          { modelId: 'openai/gpt-4', inputTokens: 500000, outputTokens: 100000 },
          { modelId: 'anthropic/claude-3-opus', inputTokens: 500000, outputTokens: 100000 },
          { modelId: 'google/gemini-pro', inputTokens: 500000, outputTokens: 100000 }
        ],
        currency: 'USD'
      })
    }
  );

  const result = await response.json();
  
  if (result.success) {
    // Sort by cost
    result.data.sort((a, b) => a.totalCost - b.totalCost);
    
    console.log('Cheapest to Most Expensive:');
    result.data.forEach(calc => {
      console.log(`${calc.modelName}: $${calc.totalCost.toFixed(8)}`);
    });
  }
}

compareCosts();
```

---

## 🔄 Supported Currencies

| Code | Currency | Symbol |
|------|----------|--------|
| USD | US Dollar | $ |
| EUR | Euro | € |
| GBP | British Pound | £ |
| JPY | Japanese Yen | ¥ |

**Note:** Prices are stored in USD and converted on request.

## ⚠️ Error Handling

### Error Codes

| Code | HTTP Status | Description |
|------|-------------|-------------|
| INVALID_MODEL | 400 | Model ID not found |
| INVALID_TOKENS | 400 | Tokens must be non-negative numbers |
| INVALID_CURRENCY | 400 | Currency not supported |
| RATE_LIMIT_EXCEEDED | 429 | Too many requests |
| SERVER_ERROR | 500 | Internal server error |

**Error Response Format:**
```json
{
  "success": false,
  "error": {
    "code": "INVALID_MODEL",
    "message": "Model 'invalid-id' not found",
    "details": "Use /api/models to get valid model IDs"
  }
}
```

**Example: Error Handling**
```javascript
async function calculateSafely(modelId, inputTokens, outputTokens) {
  try {
    const response = await fetch(
      'https://api.ai-cost-simulator.com/api/calculate',
      {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ modelId, inputTokens, outputTokens })
      }
    );

    const result = await response.json();

    if (!result.success) {
      console.error(`Error [${result.error.code}]: ${result.error.message}`);
      console.error(`Details: ${result.error.details}`);
      return null;
    }

    return result.data;

  } catch (error) {
    console.error('Network error:', error.message);
    return null;
  }
}
```

## 🔒 Rate Limiting

**Current Limits (Development):**
- No rate limits enforced

**Future Production Limits:**
- 1,000 requests per minute per IP
- 10,000 requests per day per API key
- Batch requests: max 100 items per request

## 📊 Response Times

- Calculate endpoint: < 100ms
- Get models endpoint: < 500ms
- Get model details: < 100ms

## 🌍 Data Updates

Pricing data is updated:
- Every time you access the web interface
- Every 2 days via automated GitHub Actions
- On-demand via manual trigger

## 🔗 Webhook Support (Future)

Coming soon:
- Price change notifications
- New model alerts
- Scheduled reports

## 📈 Analytics (Future)

Coming soon:
- Usage statistics
- Popular models
- Cost trends
- Provider comparison

## 🧪 Testing

### Test Models

Use these test models for development:
- `openai/gpt-4` - Always available
- `anthropic/claude-3-opus` - Always available
- `google/gemini-pro` - Always available

### Test Calculations

```bash
# Test basic calculation
curl -X POST https://api.ai-cost-simulator.com/api/calculate \
  -H "Content-Type: application/json" \
  -d '{
    "modelId": "openai/gpt-4",
    "inputTokens": 1000,
    "outputTokens": 100
  }'

# Expected response should have success: true
```

## 💡 Best Practices

1. **Cache Model Data**
   ```javascript
   let modelsCache = null;
   let cacheTime = Date.now();

   async function getModels(forceRefresh = false) {
     if (!forceRefresh && modelsCache && Date.now() - cacheTime < 3600000) {
       return modelsCache;
     }
     
     const response = await fetch('https://api.ai-cost-simulator.com/api/models');
     modelsCache = (await response.json()).data;
     cacheTime = Date.now();
     return modelsCache;
   }
   ```

2. **Handle Errors Gracefully**
   - Always check `success` flag
   - Implement retry logic for network failures
   - Use default values for missing data

3. **Batch Requests When Possible**
   - Use `/batch-calculate` for multiple models
   - Reduces total request time
   - More efficient processing

4. **Validate Input**
   - Check tokens are non-negative numbers
   - Validate currency codes
   - Verify model IDs exist

## 📞 Support & Contact

- 📧 Email: Check GitHub profile
- 💬 Discussions: [GitHub Discussions](https://github.com/mauriciomendes007/AI-Cost-Simulator-Dev/discussions)
- 🐛 Issues: [GitHub Issues](https://github.com/mauriciomendes007/AI-Cost-Simulator-Dev/issues)

## 📚 Examples Repository

Full working examples available at:
https://github.com/mauriciomendes007/AI-Cost-Simulator-Dev/tree/main/examples

## 📜 License

API and documentation are provided under the MIT License.

## 🔄 API Versioning

Current version: **v1** (Development)

Future versions will be available at:
- `/api/v2/...`
- `/api/v3/...`

---

**Last Updated**: 2026-09-12

**Status**: 🟡 In Development (Web UI ready, API in progress)

Made with ❤️ for AI integration
