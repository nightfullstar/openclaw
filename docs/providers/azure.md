---
summary: "Use Azure AI Foundry to access OpenAI, Claude, Mistral, Llama, and more"
read_when:
  - You want to run models via Azure AI Foundry in OpenClaw
  - You need enterprise-grade inference with many model providers
title: "Azure AI Foundry"
---

# Azure AI Foundry

Azure AI Foundry exposes **11,000+ models** from many providers behind a single OpenAI-compatible API. You get OpenAI, Anthropic Claude, Mistral, Meta Llama, DeepSeek, xAI Grok, Cohere, and more, all through one Azure resource and API key.

## Prerequisites

- An Azure subscription
- An Azure AI Foundry or Azure OpenAI resource
- API key from the Azure portal

## Config

Add the `azure` provider with your resource endpoint and API key:

```json5
{
  models: {
    providers: {
      azure: {
        baseUrl: "https://YOUR-RESOURCE.openai.azure.com/openai/v1",
        apiKey: "${AZURE_API_KEY}",
        models: [],
      },
    },
  },
  agents: {
    defaults: {
      model: { primary: "azure/gpt-5.2" },
    },
  },
}
```

Or use the newer Azure AI Inference endpoint:

```json5
{
  models: {
    providers: {
      azure: {
        baseUrl: "https://YOUR-RESOURCE.services.ai.azure.com",
        apiKey: "${AZURE_API_KEY}",
        models: [],
      },
    },
  },
}
```

## Model refs

Use `azure/<deployment-name>` where the deployment name matches your Azure deployment:

- `azure/gpt-5.2` — OpenAI GPT-5.2
- `azure/Mistral-Large-3` — Mistral Large 3
- `azure/claude-opus-4-6` — Anthropic Claude Opus (deployment name may vary)
- `azure/grok-3` — xAI Grok
- `azure/DeepSeek-V3.2` — DeepSeek V3.2
- `azure/Llama-3.3-70B-Instruct` — Meta Llama

Exact model IDs depend on how you named deployments in Azure. Check your Azure AI Studio or Foundry portal for deployment names.

## Auth

- **API key**: Set `AZURE_API_KEY` in the environment, or put the key in `models.providers.azure.apiKey`.
- **Auth profile**: `openclaw agents add <id>` and choose API key for provider `azure`.

## Notes

- Azure uses the OpenAI chat completions API; OpenClaw defaults to `openai-completions` for the azure provider.
- Billing goes through your Azure subscription.
- For embeddings, use the same base URL; the `/embeddings` endpoint follows the OpenAI format.
