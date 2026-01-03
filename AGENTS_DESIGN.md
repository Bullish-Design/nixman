# Agents Directory Design for nixman

## Overview

The agents directory provides a modular, extensible framework for creating specialized AI agents that collaboratively plan and scaffold NixOS configuration components. Each agent focuses on a specific domain of NixOS system configuration, enabling rapid, intelligent planning of complex system setups.

## Architecture Principles

1. **Modular Design**: Each agent is self-contained with clear boundaries
2. **Composability**: Agents can work together to plan complex configurations
3. **Rapid Scaffolding**: Template-based agent creation for quick extension
4. **Planning-First**: Agents produce plans, not implementations
5. **Knowledge Isolation**: Each agent maintains domain-specific expertise

## Directory Structure

```
agents/
├── README.md                          # Agent system documentation
├── templates/                         # Agent scaffolding templates
│   ├── base-agent.template.md        # Base agent template
│   ├── planning-agent.template.md    # Planning-focused agent template
│   └── integration-agent.template.md # Cross-domain integration agent
├── core/                             # Core system agents
│   ├── architect/                    # System architecture planning
│   │   ├── agent.md                  # Agent definition & capabilities
│   │   ├── prompts/                  # Domain-specific prompts
│   │   ├── schemas/                  # Output schemas for plans
│   │   └── examples/                 # Example plans & use cases
│   ├── orchestrator/                 # Multi-agent orchestration
│   │   ├── agent.md
│   │   ├── coordination.md           # How agents collaborate
│   │   └── workflows/                # Standard planning workflows
│   └── validator/                    # Plan validation & consistency
│       ├── agent.md
│       └── rules/                    # Validation rules
├── domain/                           # Domain-specific agents
│   ├── packages/                     # Package selection & management
│   │   ├── agent.md
│   │   ├── strategies/               # Package selection strategies
│   │   └── catalogs/                 # Package categorization
│   ├── services/                     # System services configuration
│   │   ├── agent.md
│   │   └── service-types/            # Service category templates
│   ├── hardware/                     # Hardware-specific configuration
│   │   ├── agent.md
│   │   └── profiles/                 # Hardware profiles
│   ├── network/                      # Network configuration
│   │   ├── agent.md
│   │   └── topologies/               # Network topology patterns
│   ├── security/                     # Security & hardening
│   │   ├── agent.md
│   │   └── policies/                 # Security policy templates
│   ├── users/                        # User & group management
│   │   ├── agent.md
│   │   └── personas/                 # User persona templates
│   ├── desktop/                      # Desktop environment planning
│   │   ├── agent.md
│   │   └── environments/             # DE/WM configurations
│   └── development/                  # Development environment
│       ├── agent.md
│       └── stacks/                   # Technology stack templates
├── specialized/                      # Specialized use-case agents
│   ├── homelab/                      # Homelab server planning
│   │   └── agent.md
│   ├── workstation/                  # Developer workstation
│   │   └── agent.md
│   ├── server/                       # Production server
│   │   └── agent.md
│   └── minimal/                      # Minimal system planning
│       └── agent.md
├── utilities/                        # Utility agents
│   ├── analyzer/                     # Analyze existing configs
│   │   └── agent.md
│   ├── migrator/                     # Migration planning
│   │   └── agent.md
│   └── optimizer/                    # Configuration optimization
│       └── agent.md
└── lib/                             # Shared libraries & utilities
    ├── agent-framework.md           # Agent framework documentation
    ├── communication-protocol.md    # Inter-agent communication
    ├── plan-schemas/                # Standardized plan formats
    └── knowledge-base/              # Shared NixOS knowledge
```

## Agent Anatomy

Each agent directory contains:

### 1. `agent.md` - Agent Definition
```markdown
# Agent Name

## Purpose
What this agent plans and why it exists

## Capabilities
- Specific planning capabilities
- Knowledge domains
- Decision-making authority

## Input Requirements
What information the agent needs to create plans

## Output Format
Structure of plans produced (references schema)

## Dependencies
Other agents this one collaborates with

## Invocation Patterns
When and how to activate this agent
```

### 2. Agent-Specific Resources
- **prompts/**: Domain-specific prompt templates
- **schemas/**: JSON/YAML schemas for plan outputs
- **examples/**: Example plans and use cases
- **knowledge/**: Domain-specific knowledge bases

## Agent Types

### Core Agents

#### Architect Agent
**Purpose**: High-level system architecture planning
- Determines overall system structure
- Identifies which domain agents to involve
- Creates dependency graphs between components
- Produces architectural decision records (ADRs)

#### Orchestrator Agent
**Purpose**: Coordinates multi-agent planning sessions
- Manages agent activation sequence
- Resolves conflicts between agent plans
- Ensures coherent overall configuration
- Tracks planning progress

#### Validator Agent
**Purpose**: Validates plans for consistency and feasibility
- Checks NixOS syntax correctness
- Validates inter-component dependencies
- Ensures best practices compliance
- Identifies potential conflicts

### Domain Agents

Each domain agent is an expert in one aspect of NixOS configuration:

- **Packages Agent**: Selects and organizes system packages
- **Services Agent**: Plans systemd services and daemons
- **Hardware Agent**: Hardware-specific optimizations
- **Network Agent**: Network topology and configuration
- **Security Agent**: Security hardening and policies
- **Users Agent**: User accounts and permissions
- **Desktop Agent**: Desktop environment setup
- **Development Agent**: Dev tools and environments

### Specialized Agents

Pre-configured agent combinations for common use cases:
- **Homelab Agent**: Self-hosted services planning
- **Workstation Agent**: Developer workstation setup
- **Server Agent**: Production server configuration
- **Minimal Agent**: Minimal system planning

### Utility Agents

Supporting agents for special tasks:
- **Analyzer Agent**: Analyzes existing configurations
- **Migrator Agent**: Plans migrations from other systems
- **Optimizer Agent**: Optimizes existing configurations

## Agent Creation Workflow

### Rapid Agent Scaffolding

1. **Choose Template**: Select from base/planning/integration templates
2. **Define Scope**: Specify domain and capabilities
3. **Add Knowledge**: Include domain-specific information
4. **Create Examples**: Provide reference plans
5. **Test**: Validate with sample scenarios

### Template System

#### Base Agent Template
```markdown
# [Agent Name]

## Metadata
- **Domain**: [domain]
- **Type**: [planning/analysis/integration]
- **Version**: 1.0.0
- **Dependencies**: [other agents]

## Purpose
[Clear description of what this agent plans]

## Capabilities
- [ ] Capability 1
- [ ] Capability 2

## Planning Process
1. Input gathering
2. Analysis
3. Decision making
4. Plan generation

## Output Schema
```yaml
[schema definition]
```

## Knowledge Base
[Domain-specific knowledge]

## Examples
[Example scenarios and outputs]
```

## Planning Framework

### Multi-Agent Planning Workflow

```
User Request
    ↓
Orchestrator Agent (analyzes request)
    ↓
Architect Agent (creates high-level plan)
    ↓
Orchestrator (activates relevant domain agents)
    ↓
Domain Agents (parallel planning)
    ↓
Orchestrator (integrates plans)
    ↓
Validator Agent (validates combined plan)
    ↓
Final Configuration Plan
```

### Plan Output Format

All agents produce standardized plans:

```yaml
agent: agent-name
version: 1.0.0
timestamp: ISO-8601
domain: domain-name

plan:
  summary: Brief description
  decisions:
    - decision: What was decided
      rationale: Why this decision
      alternatives: What else was considered

  components:
    - name: component-name
      type: component-type
      configuration:
        # Component-specific config
      dependencies:
        - dependency-name

  implementation_steps:
    - step: 1
      action: What to do
      files: [files affected]

  risks:
    - risk: Potential issue
      mitigation: How to address

  validation:
    - check: What to validate
      method: How to validate
```

## Inter-Agent Communication

### Communication Protocol

Agents communicate through structured messages:

```yaml
message_type: [request|response|notification]
from_agent: agent-name
to_agent: agent-name
context: planning-session-id

payload:
  # Message-specific data
```

### Coordination Patterns

1. **Sequential**: Agents work in sequence (hardware → network → services)
2. **Parallel**: Independent agents work simultaneously (packages || users)
3. **Hierarchical**: Parent agent coordinates child agents
4. **Collaborative**: Agents negotiate shared decisions

## Knowledge Management

### Shared Knowledge Base

```
lib/knowledge-base/
├── nixos/
│   ├── options-reference.md
│   ├── module-system.md
│   ├── best-practices.md
│   └── common-patterns.md
├── hardware/
│   ├── cpu-vendors.md
│   ├── gpu-vendors.md
│   └── device-drivers.md
└── software/
    ├── package-ecosystems.md
    └── service-patterns.md
```

### Agent-Specific Knowledge

Each agent maintains its own knowledge:
- Domain-specific best practices
- Common configurations
- Troubleshooting guides
- Reference examples

## Extensibility

### Adding New Agents

1. Copy appropriate template from `templates/`
2. Fill in agent-specific information
3. Add to appropriate category (core/domain/specialized/utilities)
4. Update orchestrator's agent registry
5. Add coordination rules if needed

### Agent Versioning

- Agents use semantic versioning
- Breaking changes in plan format → major version bump
- New capabilities → minor version bump
- Bug fixes → patch version bump

## Integration Points

### With nixman Core

Agents integrate with the main nixman system through:
- **Planning API**: Receive requests, return plans
- **Configuration Registry**: Access system state
- **Event Bus**: Subscribe to system events
- **File System**: Read/write plan files

### With External Tools

- **LLM Integration**: Agents use LLM capabilities via Claude Agent SDK
- **Nix Tools**: Agents can query nix-env, nix-search, etc.
- **Version Control**: Plans can be committed to git
- **Documentation**: Auto-generate docs from plans

## Example Use Cases

### Use Case 1: New Workstation Setup

```
User: "Plan a NixOS workstation for Rust development with GNOME"

Orchestrator activates:
1. Architect (overall structure)
2. Hardware (detect/optimize for hardware)
3. Desktop (GNOME setup)
4. Development (Rust toolchain)
5. Packages (supporting packages)
6. Users (user account setup)
7. Security (basic hardening)

Output: Comprehensive workstation configuration plan
```

### Use Case 2: Homelab Server

```
User: "Plan a homelab server with Docker, Jellyfin, and Nextcloud"

Orchestrator activates:
1. Architect (server architecture)
2. Services (systemd services for each app)
3. Network (reverse proxy, DNS)
4. Security (firewall, SSL certificates)
5. Packages (required packages)
6. Users (service accounts)

Output: Homelab server configuration plan
```

### Use Case 3: Migration from Ubuntu

```
User: "Help me migrate from Ubuntu to NixOS"

Orchestrator activates:
1. Analyzer (analyze Ubuntu system)
2. Migrator (create migration plan)
3. [Relevant domain agents based on analysis]
4. Validator (ensure migration feasibility)

Output: Step-by-step migration plan
```

## Quality Assurance

### Plan Quality Metrics

- **Completeness**: All required components addressed
- **Consistency**: No conflicting configurations
- **Feasibility**: Plan is implementable
- **Best Practices**: Follows NixOS conventions
- **Documentation**: Well-documented decisions

### Validation Rules

- All dependencies must be resolved
- No circular dependencies
- All referenced packages exist in nixpkgs
- Service configurations are valid
- File paths are sensible
- Security policies are enforced

## Future Enhancements

### Phase 2 Features

- **Learning Agents**: Agents that improve from user feedback
- **Simulation**: Test plans in virtual environments
- **Cost Estimation**: Estimate complexity/time for implementation
- **Conflict Resolution**: Automated conflict resolution
- **Template Generation**: Generate custom agent templates

### Phase 3 Features

- **Implementation Agents**: Agents that implement plans (not just plan)
- **Monitoring Agents**: Monitor deployed configurations
- **Optimization Agents**: Continuously optimize configurations
- **Self-Healing**: Agents that detect and fix issues

## Getting Started

### Creating Your First Agent

```bash
# 1. Copy template
cp agents/templates/planning-agent.template.md agents/domain/mynew/agent.md

# 2. Edit agent definition
vim agents/domain/mynew/agent.md

# 3. Add knowledge base
mkdir -p agents/domain/mynew/knowledge
# Add domain-specific knowledge files

# 4. Create examples
mkdir -p agents/domain/mynew/examples
# Add example plans

# 5. Register with orchestrator
# Update agents/core/orchestrator/agent-registry.yaml
```

### Testing Agents

```bash
# Test individual agent
nixman agent test packages --scenario "minimal-desktop"

# Test agent collaboration
nixman plan --agents "hardware,network,services" --dry-run

# Validate plan output
nixman validate-plan output/plan.yaml
```

## Conclusion

This agents directory design provides a flexible, extensible framework for building an intelligent NixOS configuration planning system. The modular architecture allows rapid creation of new agents while maintaining consistency and enabling powerful agent collaboration.

The planning-first approach ensures that users can iteratively refine their system design before committing to implementation, reducing errors and improving outcomes.
