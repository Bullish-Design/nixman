# nixman Agents Quick Start Guide

This guide will help you quickly understand and start using the nixman agent system for planning NixOS configurations.

## What Are nixman Agents?

nixman agents are specialized AI assistants that collaboratively plan different aspects of your NixOS system configuration. Instead of trying to configure everything at once, agents break down the complexity:

- **Architect Agent**: Plans the overall system structure
- **Packages Agent**: Selects which packages to install
- **Services Agent**: Plans systemd services configuration
- **Hardware Agent**: Handles hardware-specific setup
- **Security Agent**: Plans security hardening
- And many more...

Each agent is an expert in its domain and can work with other agents to create comprehensive, well-thought-out configuration plans.

## Core Concepts

### Planning vs Implementation

**Important**: The agent system focuses on **planning**, not implementation.

- **Planning Phase**: Agents analyze your requirements and produce detailed plans
- **Review Phase**: You review and approve plans
- **Implementation Phase**: Plans are converted to actual NixOS configurations

This approach ensures you understand and approve what's being configured before it happens.

### Agent Collaboration

Agents don't work in isolation:

```
You: "I want a Rust development workstation"
    ↓
Architect Agent: "This needs hardware, packages, desktop, and development agents"
    ↓
[Multiple agents work in parallel]
    ↓
Hardware Agent: "Detected Nvidia GPU, planning driver setup"
Packages Agent: "Planning system packages for Rust dev"
Desktop Agent: "Planning GNOME desktop environment"
Development Agent: "Planning Rust toolchain and IDE"
    ↓
Orchestrator: "Combining all plans into coherent configuration"
    ↓
Final comprehensive plan ready for review
```

## Getting Started in 5 Minutes

### 1. Basic Agent Invocation

The simplest way to use an agent:

```bash
# Plan packages for a development workstation
nixman agent invoke packages \
  --use-case workstation \
  --activities development,multimedia
```

This activates just the Packages Agent to recommend packages.

### 2. Multi-Agent Planning

For complete system planning:

```bash
# Plan a complete workstation
nixman plan \
  --use-case workstation \
  --activities development,multimedia \
  --output plan.yaml
```

This automatically:
1. Activates the Architect Agent to determine scope
2. Spawns relevant domain agents
3. Coordinates their plans
4. Produces a unified configuration plan

### 3. Review the Plan

```bash
# View the generated plan
cat plan.yaml

# Or use interactive viewer
nixman plan view plan.yaml
```

### 4. Refine the Plan

```bash
# Ask for modifications
nixman plan refine plan.yaml \
  --add "Include Docker support" \
  --remove "gaming packages"
```

### 5. Implement the Plan

```bash
# Convert plan to NixOS configuration
nixman implement plan.yaml --output /etc/nixos/
```

## Common Use Cases

### Use Case 1: New System Setup

**Scenario**: You're installing NixOS on a new laptop for development.

```bash
# Step 1: Create initial plan
nixman plan \
  --use-case workstation \
  --activities development,web-browsing,multimedia \
  --interactive

# Step 2: Answer agent questions
# Agents will ask clarifying questions:
# - "Which programming languages?" → "Rust and Python"
# - "Preferred desktop environment?" → "GNOME"
# - "Storage constraints?" → "Abundant"

# Step 3: Review generated plan
nixman plan view current-plan.yaml

# Step 4: Refine if needed
nixman plan refine current-plan.yaml --add "Include Steam for gaming"

# Step 5: Implement
nixman implement current-plan.yaml --output /etc/nixos/
```

### Use Case 2: Add New Capability

**Scenario**: You want to add Docker to existing NixOS system.

```bash
# Analyze current config and plan Docker addition
nixman agent invoke services \
  --add docker \
  --existing-config /etc/nixos/configuration.nix \
  --output docker-plan.yaml

# Review what will change
nixman plan diff /etc/nixos/configuration.nix docker-plan.yaml

# Apply changes
nixman implement docker-plan.yaml --merge /etc/nixos/configuration.nix
```

### Use Case 3: Optimize Existing Configuration

**Scenario**: Your system feels bloated, you want to optimize.

```bash
# Use analyzer and optimizer agents
nixman optimize \
  --config /etc/nixos/configuration.nix \
  --goal minimize-size \
  --output optimized-plan.yaml

# See what would be removed/changed
nixman plan diff /etc/nixos/configuration.nix optimized-plan.yaml

# Apply optimizations
nixman implement optimized-plan.yaml --output /etc/nixos/
```

### Use Case 4: Migrate from Another OS

**Scenario**: Moving from Ubuntu to NixOS, want similar setup.

```bash
# Use migrator agent to analyze Ubuntu system
nixman migrate \
  --from ubuntu \
  --analyze-packages \
  --analyze-services \
  --output migration-plan.yaml

# Review migration plan
nixman plan view migration-plan.yaml

# Adjust for NixOS best practices
nixman plan refine migration-plan.yaml --optimize-for nixos

# Implement
nixman implement migration-plan.yaml --output /etc/nixos/
```

## Understanding Agent Outputs

### Plan Structure

Every agent produces plans in this format:

```yaml
agent: packages                    # Which agent created this
version: 1.0.0
timestamp: 2024-01-15T10:30:00Z
domain: packages
session_id: sess-pkg-001

plan:
  summary: |                       # Human-readable summary
    Brief description of what this plan does

  decisions:                       # Key decisions made
    - decision: What was decided
      rationale: Why
      alternatives: What else was considered
      confidence: high/medium/low

  components:                      # What will be configured
    - name: Component name
      type: Type of component
      configuration:
        # Actual config details

  implementation_steps:            # How to implement
    - step: 1
      action: What to do
      nix_code: |
        # Actual NixOS code

  risks:                          # Potential issues
    - risk: What could go wrong
      mitigation: How to prevent

  validation_criteria:            # How to verify success
    - check: What to verify
      method: How to check
```

### Reading a Plan

Focus on these sections:

1. **Summary**: Quick overview of what this does
2. **Decisions**: Understand why choices were made
3. **Implementation Steps**: See what actually changes
4. **Risks**: Be aware of potential issues

## Creating Your Own Agent

Need a custom agent for your specific use case?

### Step 1: Copy Template

```bash
cp AGENT_TEMPLATE.md agents/domain/myagent/agent.md
```

### Step 2: Define Your Agent

Edit `agents/domain/myagent/agent.md`:

```markdown
# My Custom Agent

## Metadata
- **Domain**: domain
- **Category**: mycategory
- **Type**: planning

## Purpose
This agent plans [specific thing].

## Capabilities
- [ ] Does X
- [ ] Handles Y
- [ ] Manages Z

## Input Requirements
What information does this agent need?

## Planning Process
How does it make decisions?

## Output Format
What plans does it produce?
```

### Step 3: Add Knowledge

Create knowledge base for your agent:

```bash
mkdir -p agents/domain/myagent/knowledge
echo "# Domain-specific information" > agents/domain/myagent/knowledge/concepts.md
```

### Step 4: Create Examples

```bash
mkdir -p agents/domain/myagent/examples
```

Add example scenarios showing what your agent does.

### Step 5: Test It

```bash
nixman agent test myagent --scenario test-case-1
```

See the template file `AGENT_TEMPLATE.md` for complete details.

## Agent Directory Structure

```
agents/
├── core/              # System coordination agents
│   ├── architect/     # Overall architecture
│   ├── orchestrator/  # Multi-agent coordination
│   └── validator/     # Plan validation
│
├── domain/            # Specific domain experts
│   ├── packages/      # Package selection
│   ├── services/      # Services configuration
│   ├── hardware/      # Hardware setup
│   ├── network/       # Networking
│   ├── security/      # Security hardening
│   ├── users/         # User management
│   ├── desktop/       # Desktop environments
│   └── development/   # Dev environments
│
├── specialized/       # Pre-configured combinations
│   ├── homelab/       # Homelab servers
│   ├── workstation/   # Developer workstations
│   ├── server/        # Production servers
│   └── minimal/       # Minimal systems
│
└── utilities/         # Helper agents
    ├── analyzer/      # Analyze configs
    ├── migrator/      # Migration planning
    └── optimizer/     # Optimization
```

## Tips and Best Practices

### 1. Start with High-Level Planning

Don't jump straight to specific agents. Use the full planning workflow:

```bash
# Good: Let the system determine which agents to use
nixman plan --use-case workstation

# Less optimal: Manually invoking specific agents
nixman agent invoke packages ...
```

### 2. Use Interactive Mode for New Systems

When planning a new system, use interactive mode:

```bash
nixman plan --use-case workstation --interactive
```

This lets agents ask clarifying questions, resulting in better plans.

### 3. Review Before Implementing

Always review plans before implementing:

```bash
# Generate plan
nixman plan ... --output my-plan.yaml

# Review it thoroughly
nixman plan view my-plan.yaml

# Look for risks
grep -A 5 "risks:" my-plan.yaml

# Then implement
nixman implement my-plan.yaml
```

### 4. Iterate on Plans

Plans are meant to be refined:

```bash
# Initial plan
nixman plan --use-case workstation --output v1.yaml

# Refine
nixman plan refine v1.yaml --add "Docker support" --output v2.yaml

# Further refinement
nixman plan refine v2.yaml --remove "gaming packages" --output v3.yaml

# Implement final version
nixman implement v3.yaml
```

### 5. Use Specialized Agents for Common Patterns

Pre-configured specialized agents save time:

```bash
# Instead of manually configuring all components
nixman agent invoke specialized/homelab

# This automatically coordinates packages, services, network, security
```

### 6. Validate Plans

Always validate before implementing:

```bash
# Automatic validation
nixman validate-plan my-plan.yaml

# Manual validation checklist:
# - All dependencies resolved?
# - No conflicting packages?
# - Risks acceptable?
# - Implementation steps clear?
```

### 7. Version Control Your Plans

```bash
# Keep plans in version control
git add plans/workstation-v1.yaml
git commit -m "Initial workstation plan"

# Track iterations
git add plans/workstation-v2.yaml
git commit -m "Added Docker support"
```

## Troubleshooting

### Problem: Agent produces incomplete plan

**Solution**: Provide more detailed input

```bash
# Instead of minimal input
nixman plan --use-case workstation

# Provide detailed preferences
nixman plan \
  --use-case workstation \
  --activities development,multimedia,gaming \
  --preferences preferences.yaml \
  --hardware-info auto-detect
```

### Problem: Conflicting agent recommendations

**Solution**: The Orchestrator should resolve this automatically, but you can:

```bash
# View conflicts
nixman plan view my-plan.yaml --show-conflicts

# Manually resolve
nixman plan refine my-plan.yaml \
  --resolve-conflict "prefer packages agent recommendation"
```

### Problem: Plan fails validation

**Solution**: Check validation output

```bash
# See what failed
nixman validate-plan my-plan.yaml --verbose

# Common issues:
# - Missing dependencies: Add required components
# - Conflicting packages: Choose alternatives
# - Invalid syntax: Review generated Nix code
```

### Problem: Don't know which agent to use

**Solution**: Ask the Architect

```bash
# Let Architect determine needed agents
nixman plan --describe "I want to set up a Rust development environment"

# Architect will output which agents are needed and why
```

## Advanced Usage

### Custom Agent Workflows

Create custom workflows combining specific agents:

```yaml
# custom-workflow.yaml
workflow:
  name: minimal-dev-server
  description: Minimal server with development tools
  agents:
    - hardware
    - packages
    - development
    - security
  constraints:
    minimize_size: true
    security_level: high
```

```bash
nixman plan --workflow custom-workflow.yaml
```

### Agent Communication Inspection

See how agents collaborate:

```bash
nixman plan --use-case workstation --debug-agents
```

This shows:
- Agent activation order
- Data passed between agents
- Decision-making process
- Conflict resolution

### Plan Simulation

Test plans without applying:

```bash
# Simulate in VM
nixman simulate my-plan.yaml --vm

# Check what commands would run
nixman implement my-plan.yaml --dry-run
```

## Next Steps

1. **Read the full design**: See `AGENTS_DESIGN.md` for complete architecture
2. **Study the template**: `AGENT_TEMPLATE.md` has detailed agent structure
3. **Review examples**: `SAMPLE_PACKAGES_AGENT.md` shows real agent implementation
4. **Try it out**: Start with simple use case and expand

## Getting Help

- **Documentation**: Read agent-specific docs in `agents/*/agent.md`
- **Examples**: Check `agents/*/examples/` for reference scenarios
- **Community**: [Link to discussions/forum]
- **Issues**: [Link to issue tracker]

## Philosophy

The nixman agent system is built on these principles:

1. **Plan first, implement later**: Reduce surprises and errors
2. **Specialization**: Each agent is expert in its domain
3. **Collaboration**: Agents work together seamlessly
4. **Transparency**: Every decision is documented and explained
5. **Flexibility**: Easy to extend and customize
6. **Safety**: Validate before implementing

By following these principles, the system helps you create robust, well-planned NixOS configurations with confidence.

---

**Ready to start?** Try this:

```bash
nixman plan --use-case workstation --interactive --output my-first-plan.yaml
```

This will walk you through creating your first NixOS configuration plan!
