# cexll/myclaude: Cladue Code AI Team Workflow Sub Agents
[![](https://camo.githubusercontent.com/6cd0120cc4c5ac11d28b2c60f76033b52db98dac641de3b2644bb054b449d60c/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4c6963656e73652d4d49542d79656c6c6f772e737667)
](https://opensource.org/licenses/MIT) [![](https://camo.githubusercontent.com/d2b334f1cdcfb20cb90a9526df216a5d363f3f61befb161240b7fe0f92293726/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f436c617564652d436f64652d626c7565)
](https://claude.ai/code) [![](https://camo.githubusercontent.com/f0dc4156fe076c9350d5503464791f0bc49863898c2342993778b2832924ca5b/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f56657273696f6e2d332e322d677265656e)
](https://github.com/) [![](https://camo.githubusercontent.com/a9b4e426bb48330ff071e7d05cf7b47a6311e506ffa72d838880d8c8efc6c011/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f506c7567696e2d52656164792d707572706c65)
](https://docs.claude.com/en/docs/claude-code/plugins)

> Enterprise-grade agile development workflow automation with multi-agent orchestration

[中文](https://github.com/cexll/myclaude/blob/master/README-zh.md)

🚀 BMAD Methodology: Agile Development Automation
-------------------------------------------------

[](#-bmad-methodology-agile-development-automation)

**BMAD (Business-Minded Agile Development)** transforms your development process into a fully automated agile workflow with role-based AI agents and quality gates.

### One Command, Complete Workflow

[](#one-command-complete-workflow)

```shell
/bmad-pilot "Build e-commerce checkout system with payment integration"
# Automated: Product → Architecture → Sprint → Dev → Review → QA
```

🎯 BMAD Workflow Architecture
-----------------------------

[](#-bmad-workflow-architecture)

graph LR
    PO\[Product Owner\] -->|PRD 90+| Architect
    Architect -->|Design 90+| SM\[Scrum Master\]
    SM -->|Sprint Plan| Dev
    Dev -->|Code| Review
    Review -->|Pass/Fail| QA
    QA -->|Tests| Done

*   **🤖 6 Specialized Agents**: PO, Architect, SM, Dev, Review, QA
*   **📊 Quality Gates**: 90% thresholds with automatic optimization
*   **✅ Approval Points**: User confirmation at critical phases
*   **📁 Persistent Artifacts**: All documents saved to `./.claude/specs/`
*   **🔄 Iterative Refinement**: Automatic improvement until quality met

| Agent | Role | Quality Gate | Output |
| --- | --- | --- | --- |
| **bmad-po** (Sarah) | Product requirements gathering | 90/100 PRD score | `01-product-requirements.md` |
| **bmad-architect** (Winston) | Technical design & architecture | 90/100 design score | `02-system-architecture.md` |
| **bmad-sm** (Mike) | Sprint planning & task breakdown | User approval | `03-sprint-plan.md` |
| **bmad-dev** (Alex) | Feature implementation | Code completion | Implementation files |
| **bmad-review** | Independent code review | Pass/Risk/Fail | `04-dev-reviewed.md` |
| **bmad-qa** (Emma) | Testing & quality assurance | Test execution | `05-qa-report.md` |

#### Method 1: Plugin System (Recommended) 🎯

[](#method-1-plugin-system-recommended-)

```shell
# List available plugins
/plugin github.com/cexll/myclaude
```

#### Method 2: Traditional Installation

[](#method-2-traditional-installation)

```shell
# Clone the repository
git clone https://github.com/your-repo/claude-code-workflows.git
cd claude-code-workflows

# Install everything with make
make install

# Or deploy specific workflows
make deploy-bmad          # Deploy BMAD workflow only
make deploy-requirements  # Deploy Requirements workflow only
make deploy-all          # Deploy all commands and agents
```

```shell
# Full agile workflow with all phases
/bmad-pilot "User authentication system with OAuth2 and MFA"

# Skip testing for quick prototypes
/bmad-pilot "Admin dashboard" --skip-tests

# Direct development (skip sprint planning)
/bmad-pilot "Bug fix for login issue" --direct-dev

# Skip repository scanning (use existing context)
/bmad-pilot "Add feature" --skip-scan
```

Each BMAD run creates structured documentation:

```
.claude/specs/user-authentication/
├── 00-repository-context.md    # Repository analysis
├── 01-product-requirements.md  # PRD with business goals
├── 02-system-architecture.md   # Technical design
├── 03-sprint-plan.md           # Sprint tasks
├── 04-dev-reviewed.md          # Code review report (NEW v3.1)
└── 05-qa-report.md            # Test results 
```

The BMAD workflow uses a specialized output style that:

*   Creates phase-separated contexts
*   Manages agent handoffs
*   Tracks quality scores
*   Handles approval gates
*   Supports Codex CLI integration

### 🔌 Native Plugin Support (NEW)

[](#-native-plugin-support-new)

This project now includes native Claude Code plugin support with 4 ready-to-use plugin packages:

| Plugin | Description | Commands | Agents |
| --- | --- | --- | --- |
| **bmad-agile-workflow** | Full BMAD methodology with role-based agents | `/bmad-pilot` | bmad-po, bmad-architect, bmad-sm, bmad-dev, bmad-qa |
| **requirements-driven-development** | Streamlined requirements workflow | `/requirements-pilot` | requirements-generate, requirements-code, requirements-review |
| **development-essentials** | Core development commands | `/code`, `/debug`, `/test`, `/optimize` | code, bugfix, debug, develop |
| **advanced-ai-agents** | GPT-5 deep analysis integration | \- | gpt5 |

```shell
# List all available plugins
/plugin list

# Get detailed information about a plugin
/plugin info bmad-agile-workflow

# Install a plugin to activate its commands and agents
/plugin install requirements-driven-development

# Remove an installed plugin
/plugin remove development-essentials
```

Plugins are defined in `.claude-plugin/marketplace.json` following the Claude Code plugin specification. Each plugin includes:

*   Commands (slash commands)
*   Agents (specialized AI agents)
*   Metadata (version, author, keywords)
*   Category classification

### Independent Code Review Agent

[](#independent-code-review-agent)

*   **bmad-review**: Automated review between Dev and QA
*   **Dual Version Support**:
    *   Standard: Native Claude Code review
    *   Enhanced: GPT-5 via Codex CLI
*   **Three-tier Status**: Pass / Pass with Risk / Fail

*   Dev → Review → QA quality chain
*   Automatic Sprint plan updates
*   Targeted QA test recommendations

📊 Quality Scoring Systems
--------------------------

[](#-quality-scoring-systems)

*   Business Value: 30
*   Functional Requirements: 25
*   User Experience: 20
*   Technical Constraints: 15
*   Scope & Priorities: 10

### Architecture Quality (100 points)

[](#architecture-quality-100-points)

*   Design Quality: 30
*   Technology Selection: 25
*   Scalability: 20
*   Security: 15
*   Feasibility: 10

*   **Pass**: No issues, proceed to QA
*   **Pass with Risk**: Non-critical issues
*   **Fail**: Must return to Dev

BMAD automatically scans your repository to understand:

*   Technology stack
*   Project structure
*   Existing patterns
*   Dependencies
*   Conventions

Each phase supports iterative improvement:

```
PO: "Here's the PRD (Score: 75/100)"
User: "Add mobile support and offline mode"
PO: "Updated PRD (Score: 92/100) ✅" 
```

Critical phases require explicit confirmation:

```
Architect: "Technical design complete (Score: 93/100)"
System: "Ready to proceed? (yes/no)"
User: yes 
```

* * *

🏭 Requirements-Driven Workflow
-------------------------------

[](#-requirements-driven-workflow)

An alternative lightweight workflow for simpler projects:

```shell
/requirements-pilot "Implement JWT authentication"
# Automated: Requirements → Code → Review → Test
```

*   90% quality gates
*   Automatic optimization loops
*   Implementation-focused specs
*   Pragmatic over architectural

*   `/ask` - Technical consultation
*   `/code` - Direct implementation
*   `/debug` - Systematic debugging
*   `/test` - Testing strategies
*   `/review` - Code validation
*   `/optimize` - Performance tuning
*   `/bugfix` - Bug resolution
*   `/refactor` - Code improvement
*   `/docs` - Documentation
*   `/think` - Advanced analysis

```shell
/ask "Design patterns for real-time messaging"
/code "Implement WebSocket server"
/test "Create integration tests"
/review "Validate security"
```

MIT License - see [LICENSE](https://github.com/cexll/myclaude/blob/master/LICENSE) file

*   **Documentation**: Check `/commands/` and `/agents/` directories
*   **Plugin Guide**: See [PLUGIN\_README.md](https://github.com/cexll/myclaude/blob/master/PLUGIN_README.md) for plugin system details
*   **Issues**: GitHub issues for bugs and features
*   **Makefile Help**: Run `make help` for all deployment options
*   **Claude Code Docs**: [Plugin System](https://docs.claude.com/en/docs/claude-code/plugins)

```shell
make install              # Install everything to Claude Code
make deploy-bmad         # Deploy BMAD workflow only
make deploy-requirements # Deploy Requirements workflow only
make deploy-commands     # Deploy all slash commands
make deploy-agents       # Deploy all agent configurations
make test-bmad          # Test BMAD workflow sample
make test-requirements  # Test Requirements workflow sample
make clean              # Clean generated artifacts
make help               # Show all available commands
```

* * *

**Transform your development with BMAD** - One command, complete agile workflow, quality assured.

_Install with `/plugin install bmad-agile-workflow` or use traditional installation methods._

_Let specialized AI agents handle specialized work._