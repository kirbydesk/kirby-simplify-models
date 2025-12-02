# Kirby Simplify Models

This repository contains model information and quality ratings for AI translation providers used by the Kirby Simplify plugin.

## Structure

Each provider has its own JSON file containing:
- Provider metadata (name, website, description)
- Available models with quality ratings
- Community status (recommended, suitable, issues)

## Quality Metrics

Each model is rated on a scale of 0-100 for:

- **Translation**: Overall translation quality and accuracy
- **Context**: Understanding of context and maintaining consistency
- **Speed**: Response time and throughput
- **Cost**: Cost-effectiveness (higher = more affordable)

## Community Status

- **recommended**: Highly recommended for production use
- **suitable**: Good for most use cases
- **issues**: Known limitations or issues, use with caution

## Contributing

Feel free to submit pull requests with:
- New models
- Updated quality ratings based on real-world usage
- Corrections to provider information

## Format

```json
{
  "provider": {
    "id": "provider-id",
    "name": "Provider Name",
    "website": "https://provider.com",
    "description": "Provider description"
  },
  "models": {
    "model-id": {
      "name": "Model Display Name",
      "community_status": "recommended|suitable|issues",
      "quality": {
        "translation": 95,
        "context": 90,
        "speed": 85,
        "cost": 80
      },
      "description": "Model description"
    }
  }
}
```

## License

MIT
