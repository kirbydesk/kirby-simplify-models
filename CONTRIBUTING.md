# Contributing to Kirby Simplify Models

Thank you for your interest in contributing to the Kirby Simplify Models repository! This repository contains community-maintained model information and quality ratings for AI translation providers.

## How to Contribute

We welcome contributions in the following areas:

### 1. Adding New Models

When a provider releases a new model, you can add it to the appropriate JSON file:

**Default values for new models:**
```json
{
  "status": "unknown",
  "quality": 0,
  "recommended": false,
  "supports": ["temperature"]
}
```

**Steps:**
1. Fork the repository
2. Add the model to the appropriate provider JSON file
3. Use default values as shown above
4. Create a pull request with a clear description

### 2. Updating Model Ratings

If you have tested a model with real-world translations, you can update its ratings:

**What to update:**
- `status` - Change from "unknown" to "working" or "issues"
- `quality` - Rate from 0-5 based on translation quality
- `recommended` - Set to `true` if you recommend it for production

**Requirements:**
- Test with at least 3 different text types (e.g., technical, marketing, conversational)
- Document your testing methodology in the pull request
- Provide examples of translations if possible

### 3. Reporting Issues

If you encounter problems with a model:

**For technical issues (API errors, crashes):**
- Update `status` to "issues"
- Document the problem in the commit message
- Optionally create a GitHub issue with reproduction steps

**For quality issues:**
- Update the `quality` rating
- Explain in the commit message what problems you encountered

### 4. Adding New Providers

To add a completely new provider:

1. Create a new JSON file: `provider-name.json`
2. Follow the structure in existing files
3. Check if the provider is OpenAI-compatible or needs a custom implementation
4. Document in your PR whether plugin code changes are needed

## Guidelines

### Quality Ratings Scale

- `0` - Not yet evaluated (default)
- `1` - Low quality - frequent errors, poor context understanding
- `2` - Limited quality - usable but requires review
- `3` - Acceptable quality - good for basic translations
- `4` - Very good quality - reliable for most use cases
- `5` - Excellent quality - highly accurate and context-aware

### Status Values

- `"unknown"` - Model has not been tested yet (default)
- `"working"` - Model works reliably without known technical issues
- `"issues"` - Model has known technical problems or limitations

### Recommended Flag

- Set `recommended: true` only for models you have thoroughly tested
- Consider both quality and reliability
- Recommended models show an "Empfohlen" badge in the UI

### Testing Guidelines

Before updating ratings, test models with:
- **Technical documentation** - Accuracy with technical terms
- **Marketing content** - Tone and style preservation
- **Conversational text** - Natural language flow
- **Long-form content** - Consistency across longer texts
- **Special characters** - Handling of umlauts, emojis, etc.

## Pull Request Process

1. **Fork** the repository
2. **Create a branch** for your changes (`git checkout -b add-gpt-5-model`)
3. **Make your changes** to the JSON files
4. **Test** that the JSON is valid (use a JSON validator)
5. **Commit** with a clear message:
   - ✅ Good: "Add GPT-5 model with initial testing results (quality: 4)"
   - ❌ Bad: "Update openai.json"
6. **Push** to your fork
7. **Create a Pull Request** with:
   - Clear description of what you changed
   - Testing methodology (if updating ratings)
   - Any issues encountered

## Code of Conduct

- Be respectful and constructive
- Base ratings on objective testing, not personal preference
- Document your findings clearly
- Be open to feedback and discussion

## Questions?

If you have questions about contributing:
- Open a GitHub issue
- Check the main [README.md](README.md) for technical details
- Review existing pull requests for examples

Thank you for helping improve the Kirby Simplify Models database! 🎉
