# Kirby Simplify Models

This repository contains model information and quality ratings for AI translation providers used by the [Kirby Simplify](https://github.com/kirbydesk/kirby-simplify) plugin.

## Structure

Each provider has its own JSON file:
- `openai.json` - OpenAI models (GPT-4, GPT-3.5, etc.)
- `anthropic.json` - Anthropic models (Claude variants)
- `google.json` / `gemini.json` - Google Gemini models
- `mistral.json` - Mistral AI models
- `deepl.json` - DeepL translation service

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
- `id`: Provider identifier (openai, anthropic, google, mistral, deepl)
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

## Usage

This repository is automatically fetched by Kirby Simplify plugin via GitHub's raw content URL. The data is cached for 24 hours to reduce API calls.

## License

MIT
