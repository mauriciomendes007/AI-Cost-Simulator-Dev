# Contributing to AI Cost Simulator

Thank you for considering contributing to AI Cost Simulator! We welcome contributions from developers, AI systems, and the community.

## 📋 Code of Conduct

This project is committed to providing a welcoming and inclusive environment. By participating, you agree to maintain a respectful and professional atmosphere.

## 🚀 Getting Started

### Prerequisites
- Git installed on your system
- Modern web browser (Chrome, Firefox, Safari, Edge)
- Node.js 16+ (optional, for automation scripts)
- GitHub account

### Setup Your Development Environment

1. **Fork the Repository**
   - Visit https://github.com/mauriciomendes007/AI-Cost-Simulator-Dev
   - Click the "Fork" button in the top-right corner
   - This creates a copy under your account

2. **Clone Your Fork**
   ```bash
   git clone https://github.com/YOUR-USERNAME/AI-Cost-Simulator-Dev.git
   cd AI-Cost-Simulator-Dev
   ```

3. **Create a Feature Branch**
   ```bash
   git checkout -b feature/your-feature-name
   # or for bug fixes:
   git checkout -b fix/your-bug-name
   ```

4. **Open the Application Locally**
   ```bash
   # Option 1: Open directly in browser
   open index.html
   
   # Option 2: Use Python's built-in server
   python -m http.server 8000
   # Then visit http://localhost:8000
   
   # Option 3: Use Node's http-server
   npx http-server
   ```

## 🎯 Types of Contributions

### 🐛 Bug Reports

Found an issue? Help us fix it:

1. Go to [Issues](https://github.com/mauriciomendes007/AI-Cost-Simulator-Dev/issues)
2. Click "New Issue"
3. Use this template:

```markdown
## Bug Description
[Clear, concise description of the issue]

## Steps to Reproduce
1. Open the calculator
2. [Step 2]
3. [Step 3]
4. [Error occurs]

## Expected Behavior
[What should happen]

## Actual Behavior
[What actually happened]

## Screenshots/Video
[If applicable]

## Environment
- Browser: Chrome 120 / Firefox 121 / Safari 17 / Edge 120
- Operating System: Windows 11 / macOS 14 / Ubuntu 22.04
- Device: Desktop / Tablet / Mobile

## Additional Context
[Any other relevant information]
```

### ✨ Feature Requests

Have an idea? Share it:

1. Open a [Discussion](https://github.com/mauriciomendes007/AI-Cost-Simulator-Dev/discussions) or Issue
2. Include:

```markdown
## Feature Description
[Clear description of the feature]

## Benefit
[Why is this important? Who benefits?]

## Use Cases
- [Use case 1]
- [Use case 2]
- [Use case 3]

## Proposed Implementation
[Optional: How you might implement this]

## Acceptance Criteria
- [ ] Criterion 1
- [ ] Criterion 2
```

## 💻 Code Development

### Project Structure

```
AI-Cost-Simulator-Dev/
├── index.html                      # Main calculator application
├── package.json                    # Project metadata & dependencies
├── models-data.json               # Cached model pricing data
├── update-prices-workflow.yml      # GitHub Actions automation
├── README.md                       # Documentation (English)
├── CONTRIBUTING.md                # This file
└── .github/
    └── workflows/                 # CI/CD configurations (to be added)
```

### Code Standards

#### JavaScript Best Practices

```javascript
// Use descriptive variable names
const inputTokenCount = 50000;
const modelPricingData = { input: 0.0001, output: 0.0002 };

// Prefer const over let, avoid var
const immutableValue = 42;
let mutableValue = 0;
// const isPreferred = true; (use unless reassignment needed)

// Use arrow functions for callbacks
const calculateCost = (tokens, price) => tokens * price;

// Add comments for complex logic
// Filters out models without pricing data to prevent calculation errors
const validModels = allModels.filter(m => m.pricing?.prompt !== undefined);

// Use async/await for cleaner async code
async function fetchModelData() {
  try {
    const response = await fetch(apiUrl);
    if (!response.ok) throw new Error(`HTTP ${response.status}`);
    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Failed to fetch models:', error);
    showError('Unable to load models. Please try again.');
  }
}

// Input validation
function validateTokens(tokens) {
  if (typeof tokens !== 'number') return false;
  if (tokens < 0) return false;
  if (!isFinite(tokens)) return false;
  return true;
}
```

#### CSS Best Practices

```css
/* Use CSS variables for consistency */
:root {
  --color-primary: #667eea;
  --color-secondary: #764ba2;
  --spacing-unit: 1rem;
  --border-radius: 8px;
}

/* Mobile-first approach */
.button {
  width: 100%;
  padding: var(--spacing-unit);
}

@media (min-width: 768px) {
  .button {
    width: auto;
  }
}

/* Use BEM naming convention */
.form-group { }
.form-group__label { }
.form-group__input { }
.form-group__error { }

/* Group related styles */
.btn-primary {
  background: linear-gradient(135deg, var(--color-primary) 0%, var(--color-secondary) 100%);
  color: white;
  padding: 12px 24px;
  border-radius: var(--border-radius);
  border: none;
  cursor: pointer;
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(102, 126, 234, 0.4);
}

.btn-primary:active {
  transform: translateY(0);
}
```

### Commit Message Standards

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```bash
# Format: <type>(<scope>): <subject>

# Examples:
git commit -m "feat(calculator): add multi-currency support"
git commit -m "fix(api): correct exchange rate calculation"
git commit -m "docs(readme): update installation instructions"
git commit -m "style(css): improve button styling consistency"
git commit -m "refactor(js): simplify model loading logic"
git commit -m "perf(storage): optimize localStorage caching"
git commit -m "test(validation): add input validation tests"
```

**Valid prefixes:**
- `feat:` - New feature
- `fix:` - Bug fix
- `docs:` - Documentation
- `style:` - Code formatting (no logic changes)
- `refactor:` - Code reorganization (no behavior changes)
- `perf:` - Performance improvements
- `test:` - Testing additions
- `chore:` - Build, CI, dependencies

## 🔄 Pull Request Workflow

### 1. Make Your Changes

Edit files in your feature branch:
- **UI/Functionality**: Update `index.html`
- **Project Info**: Update `package.json`
- **Documentation**: Update `README.md` or `CONTRIBUTING.md`
- **Automation**: Update `.yml` workflow files

### 2. Test Your Changes

**Browser Testing:**
```bash
# Test in at least 2 browsers
- Chrome/Chromium (latest)
- Firefox (latest)
- Safari (if on macOS)
- Edge (if on Windows)
```

**Manual Testing Checklist:**
- [ ] Calculator loads correctly
- [ ] Models load from API
- [ ] Cost calculation works
- [ ] All currencies display correctly
- [ ] History is saved to LocalStorage
- [ ] API documentation is clear
- [ ] Mobile layout is responsive
- [ ] No console errors (F12)
- [ ] Form validation works
- [ ] Error messages display properly

### 3. Commit Your Work

```bash
git add .
git commit -m "feat(calculator): add support for JPY currency"
git commit -m "fix(api): improve error handling for failed requests"
```

Keep commits logical and focused. Avoid huge commits with multiple unrelated changes.

### 4. Push to Your Fork

```bash
git push origin feature/your-feature-name
```

### 5. Create a Pull Request

1. Visit your fork on GitHub
2. Click "Compare & pull request"
3. Fill in the PR template:

```markdown
## Description
[What does this PR do?]

## Type of Change
- [ ] New feature
- [ ] Bug fix
- [ ] Breaking change
- [ ] Documentation update

## Related Issues
Closes #123

## Testing
- [x] Tested in Chrome
- [x] Tested in Firefox
- [x] Tested on mobile
- [x] No console errors
- [x] Validation works

## Screenshots/Video
[If applicable]

## Checklist
- [x] Code follows project style
- [x] Documentation updated
- [x] No breaking changes
- [x] Tested locally
```

### 6. Code Review

- Address feedback and suggestions
- Push changes to the same branch (automatically updates PR)
- Be open to constructive criticism
- Ask questions if something is unclear

### 7. Merge

Once approved, your PR will be merged into `main` by maintainers.

## 🚀 High-Priority Features

### 🔴 Critical
- [ ] Add multiple pricing API sources (OpenAI, Anthropic, Google)
- [ ] Implement REST API backend
- [ ] Add unit tests
- [ ] Set up GitHub Actions CI/CD

### 🟡 Important
- [ ] Support more currencies
- [ ] Add comparison charts
- [ ] Export calculations to CSV/JSON
- [ ] Price history tracking
- [ ] Admin dashboard for pricing updates

### 🟢 Nice-to-Have
- [ ] Dark mode theme
- [ ] Multiple language support
- [ ] Keyboard shortcuts
- [ ] Real-time price alerts
- [ ] AI bot integration examples

## 📊 Testing

### Manual Testing Checklist

```javascript
// Test cases to verify
1. Model Loading
   - Models load on page refresh
   - Models display in dropdown
   - Model info shows pricing

2. Calculations
   - Input tokens × price = correct cost
   - Output tokens × price = correct cost
   - Total = input + output cost
   - All currencies calculate correctly

3. Validation
   - Negative numbers rejected
   - Non-numbers rejected
   - Zero values handled properly
   - Missing model shows error

4. History
   - Calculations saved to localStorage
   - History persists on refresh
   - Max 50 items stored
   - Timestamp accurate

5. UI/UX
   - Tab switching works
   - Form clearing works
   - Success/error messages display
   - Responsive on mobile
   - No console errors
```

### Browser Compatibility

Test on:
- ✅ Chrome 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+
- ✅ Mobile browsers

## 📚 Resources

### Learning
- [MDN Web Docs](https://developer.mozilla.org)
- [JavaScript.info](https://javascript.info)
- [CSS-Tricks](https://css-tricks.com)
- [GitHub Docs](https://docs.github.com)

### LLM & Pricing
- [OpenRouter API](https://openrouter.ai/docs)
- [OpenAI Pricing](https://openai.com/pricing)
- [Anthropic Claude](https://www.anthropic.com)
- [Google Vertex AI](https://cloud.google.com/vertex-ai)

### Tools
- [Git Cheat Sheet](https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf)
- [Conventional Commits](https://www.conventionalcommits.org)
- [Semantic Versioning](https://semver.org)

## 🆘 Need Help?

- 📖 **Read the Docs**: Check README.md and existing PRs
- 💬 **Ask Questions**: Use GitHub Discussions
- 🐛 **Report Issues**: Open an Issue with details
- 📧 **Contact**: Check maintainer's profile

## 🎓 Learning Path for New Contributors

1. **Start Small**
   - Read the code
   - Fix a typo in docs
   - Suggest a small improvement

2. **Make a Simple Change**
   - Add a comment
   - Fix a small bug
   - Update documentation

3. **Add a Feature**
   - Implement a planned feature
   - Add proper validation
   - Write clear commit messages

4. **Become a Maintainer**
   - Review other PRs
   - Help guide new contributors
   - Plan roadmap

## 📝 Documentation

When adding features, also update:
- **README.md**: Add to features or usage section
- **API Docs**: Update API tab in index.html if applicable
- **Comments**: Add inline comments for complex logic
- **CONTRIBUTING.md**: Update if process changes

## 🔐 Security

- Never commit API keys or secrets
- Don't expose personal information
- Report security issues privately
- Follow best practices for user data

## 🎉 Recognition

All contributors are recognized in:
- README.md Contributors section
- Release notes
- GitHub contributors page

## 📜 License

By contributing, you agree your code will be licensed under the MIT License.

## ⚖️ Legal

- Contributions must be your own work
- You grant the project rights to use your contributions
- You confirm you have authority to license the work

---

## Quick Reference

```bash
# Fork and clone
git clone https://github.com/YOUR-USERNAME/AI-Cost-Simulator-Dev.git

# Create feature branch
git checkout -b feature/description

# Make changes, test locally
# Commit with clear messages
git commit -m "type: description"

# Push to your fork
git push origin feature/description

# Create Pull Request on GitHub
# Address feedback
# Celebrate when merged! 🎉
```

**Happy Contributing!** 🚀

Questions? Open a Discussion or Issue.

Made with ❤️ by the AI Cost Simulator community
