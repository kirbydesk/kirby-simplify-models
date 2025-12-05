# Kirby Simplify Models

This repository contains model information and quality ratings for AI translation providers used by the [Kirby Simplify](https://github.com/kirbydesk/kirby-simplify) plugin.

## Available Providers

| Provider | JSON File | Plugin Implementation | API Compatibility |
|----------|-----------|----------------------|-------------------|
| **OpenAI** | `openai.json` | `OpenAI.php` | Native OpenAI API |
| **Anthropic** | `anthropic.json` | `Anthropic.php` | Native Anthropic API |
| **Google Gemini** | `gemini.json` | `Gemini.php` | Native Gemini API |
| **Mistral AI** | `mistral.json` | `OpenAI.php` | OpenAI-compatible |

### Implementation Details

- **OpenAI.php** - Handles OpenAI and OpenAI-compatible APIs (Mistral, etc.)
- **Anthropic.php** - Handles Anthropic Claude API with specific message format
- **Gemini.php** - Handles Google Gemini API with content format conversion

## Structure

Each provider has its own JSON file in the repository root:
- `openai.json` - OpenAI models (GPT-4o, GPT-4o-mini, etc.)
- `anthropic.json` - Anthropic models (Claude 3.5 Sonnet, etc.)
- `gemini.json` - Google Gemini models (Gemini 1.5 Pro, Flash, etc.)
- `mistral.json` - Mistral AI models (uses OpenAI-compatible API)

## File Format

```json
{
  "provider": {
    "id": "provider-id",
    "name": "Provider Name",
    "website": "https://provider.com"
  },
  "models": {
    "model-id": {
      "status": "working|issues|unknown",
      "quality": 0|1|2|3|4|5,
      "recommended": true|false,
      "temperature": true,
      "output_token_limit": 8192|null
    }
  }
}
```

## Fields

### Provider
- `id`: Provider identifier (must match plugin provider type)
  - `openai` - OpenAI models
  - `anthropic` - Anthropic Claude models
  - `gemini` - Google Gemini models (not "google")
  - `mistral` - Mistral AI models
- `name`: Human-readable provider name
- `url`: Provider pricing URL (e.g., pricing page)

### Model

#### `status` (string)
Technical reliability status of the model:
- `"working"` - Model works reliably without known technical issues
- `"issues"` - Model has known technical problems or limitations
- `"unknown"` - Model has not been tested yet (default for new models)

#### `quality` (number)
Translation quality rating based on real-world testing:
- `0` - Not yet evaluated (default for new models)
- `1` - Low quality - frequent errors, poor context understanding
- `2` - Limited quality - usable but requires review
- `3` - Acceptable quality - good for basic translations
- `4` - Very good quality - reliable for most use cases
- `5` - Excellent quality - highly accurate and context-aware

#### `recommended` (boolean)
Whether this model is recommended for production use:
- `true` - Recommended by the community (shown with "Empfohlen" badge in UI)
- `false` - Not specifically recommended (default for new models)

#### `temperature` (boolean)
Whether the model supports the temperature parameter for creativity control:
- `true` - Model accepts temperature parameter (typically 0.0-1.0)
- `false` - Model does not support temperature parameter

**Note:** The actual temperature value (e.g., 0.3, 0.4) is set in the variant configuration (e.g., `en.json`), not in the model config.

#### `output_token_limit` (number|null)
Maximum number of output tokens the model can generate:
- `8192` - Claude 3.5 Haiku and similar models
- `32000` - Claude Opus 4
- `64000` - Claude Sonnet 4, Claude 3.7, Haiku 4.5
- `null` - No specific limit or provider decides (OpenAI, Gemini, Mistral)

**Important:** For Anthropic models, `output_token_limit` is **required**. If not set, the API call will fail.

#### url (string|optional)
Link to model-specific documentation or information page:
- Model url - Links to specific model documentation
- If not set, can fall back to provider url
- Opens in new tab when clicked in the UI

**Examples:**
- https://platform.openai.com/docs/models/gpt-4o
- https://docs.anthropic.com/en/docs/about-claude/models
## Adding New Providers

To add a new provider:

1. **OpenAI-compatible APIs** (like Mistral):
   - Add JSON file with provider info
   - No plugin code changes needed
   - Will automatically use `OpenAI.php` implementation

2. **Custom APIs** (different format):
   - Add JSON file with provider info
   - Create new provider class in plugin (e.g., `MyProvider.php`)
   - Update `TranslationService.php` to instantiate the new class

## Usage

This repository is automatically fetched by Kirby Simplify plugin via GitHub's raw content URL:
```
https://raw.githubusercontent.com/kirbydesk/kirby-simplify-models/main/{provider}.json
```

The data is cached for 24 hours in the plugin to reduce API calls.

## Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines on:
- Adding new models
- Updating quality ratings
- Reporting issues
- Testing guidelines

## License

MIT
