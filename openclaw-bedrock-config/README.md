# OpenClaw Configuration for Amazon Bedrock

~/.openclaw/openclaw.json for Amazon Bedrock API KEY

## View Bedrock Provider Configuration

```sh
cat ~/.openclaw/openclaw.json | jq -r .models.providers.bedrock
```

```json
{
  "baseUrl": "https://bedrock-runtime.us-east-1.amazonaws.com",
  "apiKey": "${AWS_BEARER_TOKEN_BEDROCK}",
  "api": "bedrock-converse-stream",
  "auth": "api-key",
  "authHeader": true,
  "models": [
    {
      "id": "us.anthropic.claude-haiku-4-5-20251001-v1:0",
      "name": "Claude Haiku",
      "reasoning": true,
      "input": [
        "text"
      ],
      "cost": {
        "input": 0,
        "output": 0,
        "cacheRead": 0,
        "cacheWrite": 0
      },
      "contextWindow": 262144,
      "maxTokens": 8192
    }
  ]
}
```

## View Agent Defaults

```sh
cat ~/.openclaw/openclaw.json | jq -r .agents.defaults
```

```json
{
  "model": {
    "primary": "bedrock/us.anthropic.claude-haiku-4-5-20251001-v1:0"
  },
  "models": {
    "bedrock/us.anthropic.claude-haiku-4-5-20251001-v1:0": {
      "alias": "claude-haiku"
    }
  },
  ...
}
```

## Run the Gateway

```sh
export AWS_BEARER_TOKEN_BEDROCK=xxxxxxxxx
openclaw gateway run --verbose // make sure no errors
```

Now when you type `/new` in Telegram, you should see

```
✅ New session started · model: bedrock/us.anthropic.claude-haiku-4-5-20251001-v1:0
```

Then it works!

---

*Original Gist by [pahud](https://gist.github.com/pahud/8965bfeec441225009abfa96f4751f48)*
