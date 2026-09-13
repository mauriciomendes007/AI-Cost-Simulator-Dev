# AI Cost Simulator

A modern, intelligent calculator for estimating LLM API costs in real-time with global model pricing and AI bot integration support.

## 🚀 Features

✅ **Accurate Cost Calculations**
- Calculate costs based on input and output tokens
- Supports 100+ AI models globally
- Automatic pricing updates every 2 days

✅ **Global Model Database**
- Integration with OpenRouter API for real-time pricing
- Providers: OpenAI, Anthropic, Google, Meta, Mistral, Cohere, and more
- Automatic synchronization with global markets

✅ **AI Bot & Automation Integration**
- REST API for programmatic access
- Support for multiple currencies (USD, EUR, GBP, JPY)
- JSON responses for easy integration
- Designed for AI bots and automation tools

✅ **Intuitive Interface**
- Modern, responsive design
- Works on desktop, tablet, and mobile
- Fast model loading and calculations

✅ **Local History**
- Tracks last 50 calculations
- Browser LocalStorage (no server required)
- Export-ready data format

✅ **Robust Validation**
- Input validation and error handling
- Clear error messages
- Network failure resilience

## 🎯 Supported Models

Access pricing for models from:
- **OpenAI**: GPT-4, GPT-4 Turbo, GPT-3.5, Vision models
- **Anthropic**: Claude 3 (Opus, Sonnet, Haiku)
- **Google**: PaLM, Gemini Pro
- **Meta**: Llama 2, Llama 3
- **Mistral**: Mistral 7B, Medium, Large
- **Cohere**: Command, Rerank
- **And 100+ more models globally**

## 🛠️ Technology Stack

- **Frontend**: HTML5 + CSS3 + Vanilla JavaScript
- **APIs**: OpenRouter (multi-provider LLM access)
- **Storage**: Browser LocalStorage
- **Deployment**: GitHub Pages

## 📖 How to Use

### Web Interface

1. Open the calculator in your browser
2. Select an AI model from the dropdown
3. Enter:
   - **Input Tokens**: Number of tokens in your prompt
   - **Output Tokens**: Expected tokens in the response
   - **Currency**: Your preferred currency (USD, EUR, GBP, JPY)
4. Click "Calculate Cost"
5. View detailed cost breakdown

### API Integration (Coming Soon)

For AI bots and automation tools:

```javascript
const response = await fetch('https://api.ai-cost-simulator.com/calculate', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    modelId: 'openai/gpt-4',
    inputTokens: 500000,
    outputTokens: 100000,
    currency: 'USD'
  })
});

const data = await response.json();
console.log(`Total cost: ${data.data.currency}${data.data.totalCost}`);
```

See **API Docs** tab in the app for complete documentation.

## 🔄 Automatic Price Updates

The calculator:
- ✅ Reloads model list every time you access it
- ✅ Syncs prices with OpenRouter in real-time
- ✅ Updates data automatically every 2 days (GitHub Actions)
- ✅ Keeps browser cache fresh

To force a manual update:
1. Open Developer Tools (F12)
2. Run: `localStorage.clear()`
3. Reload the page

## 📊 Data Structure

```json
{
  "modelId": "openai/gpt-4",
  "name": "OpenAI GPT-4",
  "inputPrice": 0.00015,
  "outputPrice": 0.0003,
  "provider": "openai",
  "currency": "USD"
}
```

## 💼 Use Cases

- Developers estimating LLM integration costs
- Companies comparing pricing across models
- Researchers analyzing AI economics
- Startups budgeting for AI implementation
- AI bots calculating operational costs

## 🔌 For Developers & AI Bots

This project welcomes integration with AI systems:

### API Features
- Calculate costs programmatically
- Get all available models and pricing
- Multi-currency support
- JSON-based responses

### Planned Enhancements
- [ ] Additional pricing sources (Replicate, Together AI, Azure, Bedrock)
- [ ] Comparative analysis tools
- [ ] Historical price trend analysis
- [ ] Bulk cost calculations
- [ ] Custom model pricing

### How to Contribute

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Make your changes
4. Test thoroughly in multiple browsers
5. Commit with clear messages: `git commit -m "feat: add new feature"`
6. Push: `git push origin feature/your-feature`
7. Open a Pull Request

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

## 🐛 Report Issues

Found a bug? Help us improve:

1. Go to [Issues](https://github.com/mauriciomendes007/AI-Cost-Simulator-Dev/issues)
2. Click "New Issue"
3. Provide:
   - Clear description of the problem
   - Steps to reproduce
   - Expected vs actual behavior
   - Browser and OS information
   - Screenshots (if applicable)

## 📚 Pricing Data Sources

### Currently Active
- **OpenRouter API**: https://openrouter.ai/api/v1/models

### Planned Integrations
- OpenAI API
- Anthropic Bedrock
- Google Vertex AI
- Microsoft Azure OpenAI
- Replicate
- Together AI
- Hugging Face Inference

## 🌍 Currency Support

- 🇺🇸 USD - US Dollar
- 🇪🇺 EUR - Euro
- 🇬🇧 GBP - British Pound
- 🇯🇵 JPY - Japanese Yen

*More currencies coming soon*

## 📋 Project Structure

```
AI-Cost-Simulator-Dev/
├── index.html              # Main application file
├── package.json            # Project metadata
├── models-data.json        # Pricing cache (auto-updated)
├── update-prices-workflow.yml # GitHub Actions workflow
├── README.md               # This file (English)
├── CONTRIBUTING.md         # Contribution guidelines
└── .github/
    └── workflows/          # GitHub Actions (to be added)
```

## 🚀 Roadmap

### Q3 2026
- [x] English interface
- [x] Multi-currency support
- [ ] API documentation
- [ ] GitHub Pages deployment

### Q4 2026
- [ ] REST API implementation
- [ ] Additional pricing sources
- [ ] Price history tracking
- [ ] Comparison tools

### 2027
- [ ] Advanced analytics
- [ ] Export functionality
- [ ] AI bot marketplace integration
- [ ] Custom pricing models

## 📄 License

MIT License - See [LICENSE](LICENSE) file for details

This project is open source and welcomes contributions from developers and AI systems.

## 🙋 Support

- 📧 **Email**: Check the profile for contact
- 💬 **Discussions**: Use GitHub Discussions
- 🐛 **Issues**: Report bugs or request features
- 📖 **Docs**: Check [CONTRIBUTING.md](CONTRIBUTING.md)

## 🌟 Credits

**Developed by**: Mauricio Mendes
- GitHub: [@mauriciomendes007](https://github.com/mauriciomendes007)
- Repository: [AI-Cost-Simulator-Dev](https://github.com/mauriciomendes007/AI-Cost-Simulator-Dev)

## 🤝 Community

We welcome:
- Bug reports
- Feature requests
- Code contributions
- Documentation improvements
- Feedback from AI systems

---

**Status**: ✅ Active Development

**Last Updated**: Pricing data verified on each load

**For AI Bots**: This tool is designed to be integrated into AI systems for cost calculations.

Made with ❤️ for developers and AI systems worldwide
