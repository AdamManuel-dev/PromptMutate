# PromptMutate 🧬

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Node.js Version](https://img.shields.io/badge/node-%3E%3D20.0.0-brightgreen)](https://nodejs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue)](https://www.typescriptlang.org/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

An intelligent prompt optimization system that automatically improves AI code generation through mutation testing, deterministic scoring, and adaptive learning. PromptMutate transforms manual prompt engineering into a data-driven, continuous optimization process.

This is a PoC/MVP for [SyntaxLabs](https://github.com/AdamManuel-dev/SyntaxLab)

## 🚀 Key Features

- **🧪 Automated A/B Testing**: Statistical testing of prompt variations with automatic winner selection
- **🔬 Mutation Engine**: Intelligent prompt mutations across token, structure, and semantic levels
- **📊 Deterministic Scoring**: Multi-metric code quality evaluation with reproducible results
- **🎯 Multi-Armed Bandits**: Efficient resource allocation using advanced optimization algorithms
- **🔄 Continuous Learning**: Pattern recognition and knowledge accumulation from successful prompts
- **🤖 Claude Code Integration**: Seamless integration with Claude and other AI coding assistants
- **📈 Real-time Analytics**: Comprehensive dashboards for tracking prompt performance

## 📋 Table of Contents

- [Quick Start](#-quick-start)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Usage](#-usage)
- [Architecture](#-architecture)
- [API Reference](#-api-reference)
- [Scoring Metrics](#-scoring-metrics)
- [Mutation Strategies](#-mutation-strategies)
- [Integration Guide](#-integration-guide)
- [Contributing](#-contributing)
- [Troubleshooting](#-troubleshooting)
- [License](#-license)

## 🏃 Quick Start

```bash
# Install PromptMutate
npm install -g promptmutate

# Initialize configuration
promptmutate init

# Create your first prompt
promptmutate create --name "react-component" --file prompts/react.txt

# Start optimization
promptmutate optimize --prompt "react-component" --target "mutation-score:90"

# View results
promptmutate dashboard
```

## 💾 Installation

### Prerequisites

- Node.js >= 20.0.0
- PostgreSQL >= 14
- Redis >= 7.0
- Docker (optional, for containerized deployment)

### From NPM

```bash
npm install -g promptmutate
```

### From Source

```bash
# Clone the repository
git clone https://github.com/yourusername/promptmutate.git
cd promptmutate

# Install dependencies
npm install

# Build the project
npm run build

# Link for global usage
npm link
```

### Docker Installation

```bash
# Using Docker Compose
docker-compose up -d

# Or using individual containers
docker run -d --name promptmutate-db postgres:14
docker run -d --name promptmutate-redis redis:7
docker run -d --name promptmutate \
  -e DATABASE_URL=postgresql://... \
  -e REDIS_URL=redis://... \
  promptmutate/promptmutate:latest
```

## ⚙️ Configuration

### Environment Variables

Create a `.env` file in your project root:

```env
# Database
DATABASE_URL=postgresql://user:password@localhost:5432/promptmutate
REDIS_URL=redis://localhost:6379

# Claude API
CLAUDE_API_KEY=your-claude-api-key
CLAUDE_MODEL=claude-3-opus-20240229

# Vector Database (optional)
CHROMA_URL=http://localhost:8000

# Monitoring (optional)
PROMETHEUS_PORT=9090
GRAFANA_URL=http://localhost:3000

# Feature Flags
ENABLE_MUTATIONS=true
ENABLE_SEMANTIC_ANALYSIS=true
ENABLE_COST_OPTIMIZATION=true
```

### Configuration File

Create `promptmutate.config.yml`:

```yaml
# Scoring Configuration
scoring:
  weights:
    correctness: 0.35
    mutationScore: 0.20
    complexity: 0.15
    performance: 0.15
    security: 0.10
    similarity: 0.05
  
  thresholds:
    minimum_quality: 0.7
    production_ready: 0.85

# Mutation Configuration
mutation:
  strategies:
    - token_replacement
    - structure_modification
    - semantic_enhancement
  
  rate: 0.1  # 10% mutation rate
  max_variants: 50
  
  token_mutations:
    synonym_probability: 0.3
    emphasis_probability: 0.2
    quantifier_probability: 0.1

# Optimization Configuration
optimization:
  algorithm: "thompson_sampling"  # or "epsilon_greedy", "ucb"
  exploration_rate: 0.2
  convergence_threshold: 0.95
  min_samples: 100

# Integration Configuration
integrations:
  claude:
    model: "claude-3-opus-20240229"
    max_tokens: 4000
    temperature: 0.2
    cache_enabled: true
  
  github:
    actions_enabled: true
    pr_comments: true
    
  task_kanban_mcp:
    endpoint: "http://localhost:3000"
    api_key: "your-mcp-api-key"

# Monitoring Configuration
monitoring:
  metrics_retention: "90d"
  log_level: "info"
  alerts:
    - metric: "success_rate"
      threshold: 0.8
      operator: "less_than"
    - metric: "api_cost"
      threshold: 1000
      operator: "greater_than"
```

## 📖 Usage

### CLI Commands

#### Prompt Management

```bash
# Create a new prompt
promptmutate create --name "api-endpoint" --file prompt.txt --tags "backend,rest"

# List all prompts
promptmutate list --filter "active" --sort "performance"

# Update a prompt
promptmutate update --id prompt-123 --file updated-prompt.txt

# View prompt details
promptmutate show --name "api-endpoint" --include-metrics
```

#### Experimentation

```bash
# Start an A/B test
promptmutate experiment start \
  --name "react-optimization" \
  --variants "prompt-v1,prompt-v2" \
  --duration "7d" \
  --traffic-split "50,50"

# Check experiment status
promptmutate experiment status --name "react-optimization"

# Stop experiment early
promptmutate experiment stop --name "react-optimization" --declare-winner
```

#### Mutation Operations

```bash
# Generate mutations for a prompt
promptmutate mutate \
  --prompt "api-endpoint" \
  --strategy "aggressive" \
  --count 10

# Test mutations
promptmutate test-mutations \
  --prompt "api-endpoint" \
  --iterations 5 \
  --parallel 3

# Apply best mutation
promptmutate apply-mutation \
  --prompt "api-endpoint" \
  --mutation "mut-789"
```

#### Analysis and Reporting

```bash
# Analyze code quality
promptmutate analyze \
  --code "path/to/generated/code" \
  --language "typescript" \
  --detailed

# Generate performance report
promptmutate report \
  --period "last-7d" \
  --format "pdf" \
  --output "report.pdf"

# Export successful patterns
promptmutate export-patterns \
  --min-score 0.9 \
  --format "json" \
  --output "patterns.json"
```

### Programmatic API

```typescript
import { PromptMutate } from 'promptmutate';

// Initialize the client
const pm = new PromptMutate({
  apiKey: process.env.PROMPTMUTATE_API_KEY,
  baseUrl: 'http://localhost:3000'
});

// Create and optimize a prompt
async function optimizePrompt() {
  // Create a base prompt
  const prompt = await pm.prompts.create({
    name: 'user-auth-component',
    content: 'Create a React component for user authentication...',
    tags: ['react', 'auth', 'frontend']
  });

  // Start optimization
  const optimization = await pm.optimize({
    promptId: prompt.id,
    targetMetrics: {
      mutationScore: 0.9,
      complexity: { max: 10 }
    },
    maxIterations: 100
  });

  // Monitor progress
  optimization.on('iteration', (result) => {
    console.log(`Iteration ${result.iteration}: Score ${result.score}`);
  });

  // Get the optimized prompt
  const optimized = await optimization.result();
  console.log('Optimized prompt:', optimized.content);
}

// Integrate with Claude Code
async function generateWithOptimizedPrompt(task: string) {
  // Get the best prompt for the task type
  const prompt = await pm.prompts.getBest({
    taskType: 'react-component',
    context: { framework: 'react', typescript: true }
  });

  // Use with Claude
  const result = await claudeCode.generate({
    prompt: prompt.content,
    task: task
  });

  // Report metrics back
  await pm.metrics.report({
    promptId: prompt.id,
    generatedCode: result.code,
    success: result.success,
    executionTime: result.duration
  });

  return result;
}
```

## 🏗️ Architecture

### System Overview

```
┌─────────────────────────────────────────────────────────────┐
│                     User Interface Layer                     │
│          (CLI, Web Dashboard, REST API, GraphQL)            │
└─────────────────────────────┬───────────────────────────────┘
                              │
┌─────────────────────────────▼──────────────────────────────┐
│                  Orchestration Engine                      │
│         (Experiment Management, Task Distribution)         │
├─────────────┬────────────────┬────────────────┬────────────┤
│   Prompt    │   Mutation     │   Evaluation   │  Learning  │
│  Manager    │   Engine       │   Engine       │  Engine    │
├─────────────┼────────────────┼────────────────┼────────────┤
│ • Storage   │ • Strategies   │ • AST Parser   │ • Patterns │
│ • Versions  │ • Generator    │ • Mutation Test│ • ML Models│
│ • Templates │ • Validator    │ • Scoring      │ • Analytics│
└─────────────┴────────────────┴────────────────┴────────────┘
                              │
┌─────────────────────────────▼───────────────────────────────┐
│                    Integration Layer                        │
├──────────────┬───────────────┬───────────────┬──────────────┤
│  Claude API  │  Git Analysis │  CI/CD Hooks  │   MCP        │
│              │               │  (GitHub/GL)  │   Protocol   │
└──────────────┴───────────────┴───────────────┴──────────────┘
                              │
┌─────────────────────────────▼──────────────────────────────┐
│                      Data Layer                            │
├──────────────┬───────────────┬───────────────┬─────────────┤
│  PostgreSQL  │    Redis      │  ChromaDB     │   S3        │
│  (Metadata)  │   (Cache)     │ (Embeddings)  │ (Artifacts) │
└──────────────┴───────────────┴───────────────┴─────────────┘
```

### Component Descriptions

- **Orchestration Engine**: Manages experiments, distributes tasks, and coordinates all subsystems
- **Prompt Manager**: Handles CRUD operations, versioning, and template management
- **Mutation Engine**: Generates intelligent variations using multiple strategies
- **Evaluation Engine**: Performs multi-metric scoring including AST analysis and mutation testing
- **Learning Engine**: Identifies patterns, clusters successful prompts, and builds knowledge base

## 📚 API Reference

### REST API Endpoints

```bash
# Prompt Management
POST   /api/v1/prompts              # Create prompt
GET    /api/v1/prompts              # List prompts
GET    /api/v1/prompts/:id          # Get prompt
PUT    /api/v1/prompts/:id          # Update prompt
DELETE /api/v1/prompts/:id          # Delete prompt

# Experiments
POST   /api/v1/experiments          # Start experiment
GET    /api/v1/experiments          # List experiments
GET    /api/v1/experiments/:id      # Get experiment
PATCH  /api/v1/experiments/:id      # Update experiment
DELETE /api/v1/experiments/:id      # Stop experiment

# Evaluation
POST   /api/v1/evaluate             # Evaluate code
GET    /api/v1/metrics/:promptId    # Get metrics

# Mutations
POST   /api/v1/mutate               # Generate mutations
GET    /api/v1/mutations/:promptId  # List mutations
POST   /api/v1/mutations/:id/apply  # Apply mutation
```

### WebSocket Events

```javascript
// Connect to WebSocket
const ws = new WebSocket('ws://localhost:3000/ws');

// Subscribe to events
ws.send(JSON.stringify({
  type: 'subscribe',
  channels: ['experiments', 'mutations', 'metrics']
}));

// Receive real-time updates
ws.on('message', (data) => {
  const event = JSON.parse(data);
  switch(event.type) {
    case 'experiment.update':
      console.log('Experiment progress:', event.data);
      break;
    case 'mutation.generated':
      console.log('New mutation:', event.data);
      break;
    case 'metrics.updated':
      console.log('Metrics update:', event.data);
      break;
  }
});
```

## 📊 Scoring Metrics

### Quality Score Calculation

```typescript
// Composite score formula
QualityScore = Σ(weight_i × normalize(metric_i))

// Default weights
const weights = {
  correctness: 0.35,      // Test pass rate
  mutationScore: 0.20,    // Killed mutants / total mutants
  complexity: 0.15,       // Cyclomatic complexity (inverted)
  performance: 0.15,      // Execution time benchmarks
  security: 0.10,         // Vulnerability scan results
  similarity: 0.05        // AST similarity to best practices
};
```

### Metric Details

1. **Correctness** (35%)
   - Unit test pass rate
   - Integration test success
   - Type checking results
   - Linting compliance

2. **Mutation Score** (20%)
   ```
   Mutation Score = Killed Mutants / (Total Mutants - Equivalent Mutants)
   ```
   - Arithmetic mutations
   - Conditional mutations
   - Return value mutations
   - Method call mutations

3. **Complexity** (15%)
   - Cyclomatic complexity
   - Cognitive complexity
   - Lines of code
   - Nesting depth

4. **Performance** (15%)
   - Execution time
   - Memory usage
   - Time complexity
   - Space complexity

5. **Security** (10%)
   - OWASP compliance
   - Dependency vulnerabilities
   - Code injection risks
   - Authentication checks

6. **Similarity** (5%)
   - AST edit distance
   - Pattern matching
   - Best practice alignment
   - Style consistency

## 🧬 Mutation Strategies

### Token-Level Mutations

```typescript
// Example: Synonym replacement
Original: "Create a function to calculate"
Mutated:  "Develop a function to compute"

// Example: Emphasis addition
Original: "Handle errors gracefully"
Mutated:  "ALWAYS handle errors gracefully"

// Example: Quantifier modification
Original: "Add some validation"
Mutated:  "Add comprehensive validation"
```

### Structure-Level Mutations

```typescript
// Example: Reordering
Original: "Create a React component with state management and API calls"
Mutated:  "Create a React component with API calls and state management"

// Example: List formatting
Original: "Include error handling, logging, and validation"
Mutated:  
"Include:
- Error handling
- Logging functionality  
- Input validation"
```

### Semantic-Level Mutations

```typescript
// Example: Context expansion
Original: "Build a user authentication form"
Mutated:  "Build a secure user authentication form with proper input validation, 
           error handling, and accessibility features following WCAG guidelines"

// Example: Constraint modification
Original: "Optimize for performance"
Mutated:  "Optimize for performance while maintaining code readability"
```

## 🔗 Integration Guide

### Claude Code Integration

```typescript
// 1. Install the integration package
npm install @promptmutate/claude-integration

// 2. Configure in your Claude Code setup
import { PromptMutateIntegration } from '@promptmutate/claude-integration';

const integration = new PromptMutateIntegration({
  apiKey: process.env.PROMPTMUTATE_API_KEY,
  autoOptimize: true,
  reportMetrics: true
});

// 3. Use in your workflow
claudeCode.use(integration.middleware());
```

### CI/CD Integration

```yaml
# GitHub Actions Example
name: Prompt Optimization
on:
  pull_request:
    paths:
      - 'prompts/**'

jobs:
  optimize:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup PromptMutate
        uses: promptmutate/setup-action@v1
        with:
          api-key: ${{ secrets.PROMPTMUTATE_API_KEY }}
      
      - name: Run Optimization
        run: |
          promptmutate optimize \
            --config .promptmutate.yml \
            --target "mutation-score:85" \
            --max-time "30m"
      
      - name: Comment Results
        uses: promptmutate/pr-comment@v1
        with:
          report-file: optimization-report.json
```

### Task-Kanban-MCP Integration

```typescript
// Configure MCP tools
const mcpTools = [
  {
    name: "get_optimized_prompt",
    description: "Get the best performing prompt for a task",
    handler: async ({ taskType, context }) => {
      const prompt = await promptMutate.prompts.getBest({
        taskType,
        context
      });
      return prompt.content;
    }
  },
  {
    name: "report_code_quality",
    description: "Report quality metrics for generated code",
    handler: async ({ promptId, metrics }) => {
      await promptMutate.metrics.report({
        promptId,
        ...metrics
      });
    }
  }
];
```

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

### Development Setup

```bash
# Clone the repository
git clone https://github.com/yourusername/promptmutate.git
cd promptmutate

# Install dependencies
npm install

# Set up databases
docker-compose up -d postgres redis

# Run migrations
npm run db:migrate

# Start development server
npm run dev

# Run tests
npm test

# Run mutation tests
npm run test:mutation
```

### Coding Standards

- TypeScript for all source code
- ESLint + Prettier for formatting
- Jest for unit tests
- Stryker for mutation testing
- Conventional commits

### Pull Request Process

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'feat: add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 🔧 Troubleshooting

### Common Issues

#### High API Costs
```bash
# Enable cost optimization
promptmutate config set optimization.cost_aware true

# Set daily budget
promptmutate config set daily_budget 50

# Use caching aggressively
promptmutate config set cache.ttl 3600
```

#### Low Mutation Scores
```bash
# Increase mutation diversity
promptmutate config set mutation.strategies "all"

# Adjust mutation rate
promptmutate config set mutation.rate 0.2

# Enable semantic mutations
promptmutate config set mutation.semantic_enabled true
```

#### Slow Evaluations
```bash
# Enable parallel processing
promptmutate config set evaluation.parallel true
promptmutate config set evaluation.workers 8

# Use incremental testing
promptmutate config set testing.incremental true
```

### Debug Mode

```bash
# Enable debug logging
export PROMPTMUTATE_LOG_LEVEL=debug

# Run with verbose output
promptmutate --verbose optimize --prompt "my-prompt"

# Generate debug report
promptmutate debug --include-logs --output debug-report.zip
```

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [Stryker Mutator](https://stryker-mutator.io/) for mutation testing inspiration
- [DSPy](https://dspy.ai/) for prompt optimization techniques
- [Claude](https://anthropic.com) for outstanding code generation capabilities
- The open-source community for continuous feedback and contributions

## 📞 Support

- 📧 Email: support@promptmutate.io
- 💬 Discord: [Join our community](https://discord.gg/promptmutate)
- 📖 Documentation: [docs.promptmutate.io](https://docs.promptmutate.io)
- 🐛 Issues: [GitHub Issues](https://github.com/yourusername/promptmutate/issues)

---

Built with ❤️ by developers, for developers. Make your AI agents smarter, one mutation at a time! 🚀
