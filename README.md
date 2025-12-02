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
      "status": "working|issues",
      "quality": 5,
      "supports": ["temperature"]
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
- `website`: Provider's website URL

### Model
- `status`: Model status
  - `working` - Model works reliably
  - `issues` - Known problems or limitations
- `quality`: Translation quality rating (1-5 scale)
  - `5` - Excellent quality
  - `4` - Very good quality
  - `3` - Acceptable quality
  - `2` - Limited quality
  - `1` - Low quality
- `supports`: Array of supported features
  - `temperature` - Supports temperature parameter for creativity control
  - Can be empty array `[]` if no special features

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

## Contributing

Contributions are welcome! Please submit pull requests with:
- New models as they become available
- Updated quality ratings based on real-world translation experience
- Status updates (working ↔ issues)
- Corrections to provider information

### Guidelines
- Quality ratings should reflect translation accuracy and consistency
- Status should only be marked as "issues" if there are reproducible problems
- Test models with actual translation tasks before rating
- Ensure provider `id` matches the plugin's expected provider type

## Usage

This repository is automatically fetched by Kirby Simplify plugin via GitHub's raw content URL:
```
https://raw.githubusercontent.com/kirbydesk/kirby-simplify-models/main/{provider}.json
```

The data is cached for 24 hours in the plugin to reduce API calls.

## License

MIT
