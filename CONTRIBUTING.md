# Guia de Contribuição - AI Cost Simulator

Obrigado por considerar contribuir para o AI Cost Simulator! Este documento fornece diretrizes e instruções para ajudar no desenvolvimento do projeto.

## 📋 Código de Conduta

Este projeto adere a um Código de Conduta. Ao participar, você concorda em manter um ambiente respeitoso e inclusivo.

## 🚀 Como Começar

### Pré-requisitos
- Git instalado
- Navegador web moderno (Chrome, Firefox, Safari, Edge)
- Node.js 16+ (opcional, para scripts)
- Conta GitHub

### Configuração do Ambiente

1. **Fork o repositório**
   ```bash
   # Visite https://github.com/mauriciomendes007/AI-Cost-Simulator-Dev
   # Clique em "Fork" no canto superior direito
   ```

2. **Clone seu fork**
   ```bash
   git clone https://github.com/SEU-USUARIO/AI-Cost-Simulator-Dev.git
   cd AI-Cost-Simulator-Dev
   ```

3. **Crie uma branch para sua feature**
   ```bash
   git checkout -b feature/sua-feature
   # ou
   git checkout -b fix/seu-bugfix
   ```

4. **Abra `index.html` no navegador**
   ```bash
   # Abra direto ou use um servidor local
   python -m http.server 8000
   # Acesse http://localhost:8000
   ```

## 🎯 Tipos de Contribuições

### 🐛 Relatórios de Bugs

Encontrou um bug? Abra uma issue com:

```markdown
## Descrição do Bug
[Descrição clara do problema]

## Passos para Reproduzir
1. Abra a calculadora
2. [passo 2]
3. [passo 3]

## Comportamento Esperado
[O que deveria acontecer]

## Comportamento Atual
[O que está acontecendo]

## Screenshots
[Se aplicável]

## Ambiente
- Browser: [Chrome, Firefox, Safari]
- SO: [Windows, macOS, Linux]
- Versão: [se aplicável]
```

### ✨ Novas Funcionalidades

Tem uma ideia? Abra uma issue primeiro para discussão:

```markdown
## Descrição da Feature
[Descrição clara da funcionalidade]

## Benefício
[Por que isso é importante?]

## Casos de Uso
- [Caso 1]
- [Caso 2]

## Possível Implementação
[Se tiver ideias, compartilhe]
```

## 💻 Desenvolvimento

### Estrutura do Projeto

```
AI-Cost-Simulator-Dev/
├── index.html              # Arquivo principal da aplicação
├── package.json            # Metadados do projeto
├── models-data.json        # Cache de preços dos modelos
├── update-prices-workflow.yml # Workflow de atualização
├── README.md               # Documentação principal
├── CONTRIBUTING.md         # Este arquivo
└── .github/
    └── workflows/          # GitHub Actions (a ser configurado)
```

### Arquitetura

**Frontend**: HTML + CSS + Vanilla JavaScript
- Sem dependências externas
- Usa LocalStorage para dados persistentes
- Integra com OpenRouter API

**Backend**: GitHub Actions (opcional)
- Atualiza preços automaticamente
- Executa a cada 2 dias

### Padrões de Código

#### JavaScript
```javascript
// Use nomes descritivos
function calcularCustoTotal() { }

// Use const por padrão
const modelo = precosModelos[modelId];

// Adicione comentários para lógica complexa
// Filtra modelos que têm preço definido
const modelosValidos = data.filter(m => m.pricing?.prompt);

// Use async/await
async function carregarDados() {
  try {
    const response = await fetch(url);
    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Erro:', error);
  }
}
```

#### CSS
```css
/* Use variáveis CSS */
:root {
  --cor-primaria: #667eea;
  --cor-secundaria: #764ba2;
  --espacamento: 1rem;
}

/* Mobile-first */
.container {
  width: 100%;
}

@media (min-width: 768px) {
  .container {
    max-width: 900px;
  }
}

/* BEM naming */
.btn-calcular { }
.btn-calcular:hover { }
```

## 🔄 Workflow de Contribuição

### 1. Faça suas mudanças

Edite os arquivos necessários:
- **index.html**: Para interface/lógica
- **package.json**: Para metadados
- **README.md**: Para documentação
- **update-prices-workflow.yml**: Para automação

### 2. Teste suas mudanças

```bash
# Abra em múltiplos navegadores
# Teste em mobile também
# Verifique o console (F12) para erros
```

### 3. Commit com mensagens claras

```bash
git add .
git commit -m "feat: adicionar suporte para moedas múltiplas"
# ou
git commit -m "fix: corrigir cálculo de tokens"
# ou
git commit -m "docs: atualizar guia de contribuição"
```

**Prefixos recomendados:**
- `feat:` - Nova funcionalidade
- `fix:` - Correção de bug
- `docs:` - Documentação
- `style:` - Formatação (sem lógica)
- `refactor:` - Refatoração
- `test:` - Testes
- `perf:` - Performance
- `chore:` - Tarefas administrativas

### 4. Push para seu fork

```bash
git push origin feature/sua-feature
```

### 5. Abra um Pull Request

- Vá para https://github.com/mauriciomendes007/AI-Cost-Simulator-Dev
- Clique em "New Pull Request"
- Selecione sua branch
- Preencha o template:

```markdown
## Descrição
[O que esta PR faz?]

## Tipo de Mudança
- [ ] Nova funcionalidade
- [ ] Correção de bug
- [ ] Mudança que quebra compatibilidade
- [ ] Atualização de documentação

## Checklist
- [ ] Testei no Chrome
- [ ] Testei no Firefox
- [ ] Testei em mobile
- [ ] Atualizei a documentação
- [ ] Meu código segue o estilo do projeto

## Screenshots/Video
[Se aplicável]

## Issues Relacionadas
Closes #123
```

## 📊 Melhorias Prioritárias

### 🔴 Alta Prioridade
- [ ] Adicionar mais fontes de preços (OpenAI, Anthropic, Google)
- [ ] Suporte para múltiplas moedas
- [ ] Gráficos comparativos entre modelos
- [ ] Exportar histórico em CSV/JSON

### 🟡 Média Prioridade
- [ ] Integração com APIs de billing reais
- [ ] Análise de tendências de preço
- [ ] Favoritar modelos
- [ ] Compartilhar cálculos

### 🟢 Baixa Prioridade
- [ ] Temas (light/dark)
- [ ] Múltiplos idiomas
- [ ] Atalhos de teclado
- [ ] Notificações de mudança de preço

## 🔧 Scripts Úteis

```bash
# Atualizar preços manualmente
node update-prices.js

# Verificar sintaxe (se tiver Node.js)
npm test

# Limpar histórico (execute no console do navegador)
localStorage.clear()
```

## 📝 Documentação

### Comentar Código
```javascript
/**
 * Calcula o custo total baseado em tokens
 * @param {number} inputTokens - Tokens de entrada
 * @param {number} outputTokens - Tokens de saída
 * @param {Object} priceData - Dados de preço do modelo
 * @returns {number} Custo total em USD
 */
function calcularCusto(inputTokens, outputTokens, priceData) {
  return (inputTokens * priceData.input) + (outputTokens * priceData.output);
}
```

### README
- Mantenha atualizado com novas features
- Adicione exemplos de uso
- Explique mudanças importantes

## 🧪 Testes

### Teste Manual
1. Abra a calculadora
2. Teste cada funcionalidade
3. Verifique em múltiplos navegadores
4. Teste responsividade (mobile)
5. Verifique console para erros

### Casos de Teste
```javascript
// Teste casos extremos
- Valores 0
- Valores muito grandes
- Caracteres especiais
- Sem modelo selecionado
- Conexão de rede perdida
```

## 🚨 Reporting Issues

### Template de Issue

```markdown
**Tipo**: [Bug | Feature | Documentação | Pergunta]

**Descrição**
[Descrição clara do problema]

**Contexto**
- Browser: [versão]
- SO: [versão]
- URL de referência: [se aplicável]

**Solução Proposta**
[Se tiver ideias]
```

## 📚 Recursos Úteis

- [OpenRouter API Docs](https://openrouter.ai/docs)
- [MDN Web Docs](https://developer.mozilla.org)
- [Git Cheat Sheet](https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf)
- [Conventional Commits](https://www.conventionalcommits.org)

## 🎓 Aprenda Mais

### Sobre LLMs e Preços
- [OpenAI Pricing](https://openai.com/pricing)
- [Anthropic Claude](https://www.anthropic.com)
- [Google Vertex AI](https://cloud.google.com/vertex-ai)

### Sobre Desenvolvimento Web
- [HTML5 Specification](https://html.spec.whatwg.org)
- [CSS-Tricks](https://css-tricks.com)
- [JavaScript.info](https://javascript.info)

## 🏆 Reconhecimento

Todos os contribuidores serão reconhecidos em:
- README.md (seção de contribuidores)
- Release notes

## ❓ Dúvidas?

- 💬 Abra uma discussion no GitHub
- 📧 Verifique o perfil para contato
- 🐛 Abra uma issue para esclarecimentos

## 📜 Licença

Ao contribuir, você concorda que suas contribuições serão licenciadas sob a MIT License.

---

**Obrigado por contribuir!** 🙏

Qualquer dúvida, abra uma issue ou discussion. Feliz codificação! 🚀
