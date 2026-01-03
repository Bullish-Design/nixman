# nixman Agents Directory Structure

This document provides the complete directory structure for the nixman agent system. Use this as a reference when creating the actual directories and files.

## Complete Directory Tree

```
agents/
│
├── README.md                                 # Main documentation for agent system
│
├── templates/                                # Templates for creating new agents
│   ├── base-agent.template.md              # Minimal agent template
│   ├── planning-agent.template.md          # Planning-focused agent template
│   ├── integration-agent.template.md       # Cross-domain integration agent template
│   └── specialized-agent.template.md       # Pre-configured specialized agent template
│
├── core/                                     # Core system agents (orchestration & coordination)
│   │
│   ├── architect/                           # System architecture planning
│   │   ├── agent.md                        # Agent definition
│   │   ├── prompts/                        # Domain-specific prompts
│   │   │   ├── system-analysis.md
│   │   │   ├── dependency-mapping.md
│   │   │   └── architecture-decision.md
│   │   ├── schemas/                        # Output schemas
│   │   │   ├── architecture-plan.yaml
│   │   │   └── component-graph.yaml
│   │   └── examples/                       # Example plans
│   │       ├── workstation-architecture.yaml
│   │       ├── server-architecture.yaml
│   │       └── homelab-architecture.yaml
│   │
│   ├── orchestrator/                        # Multi-agent orchestration & coordination
│   │   ├── agent.md                        # Agent definition
│   │   ├── coordination.md                 # How agents collaborate
│   │   ├── workflows/                      # Standard planning workflows
│   │   │   ├── new-system-workflow.yaml
│   │   │   ├── migration-workflow.yaml
│   │   │   ├── optimization-workflow.yaml
│   │   │   └── incremental-change-workflow.yaml
│   │   ├── agent-registry.yaml             # Registry of all available agents
│   │   └── conflict-resolution.md          # Strategies for resolving agent conflicts
│   │
│   └── validator/                           # Plan validation & consistency checking
│       ├── agent.md                        # Agent definition
│       ├── rules/                          # Validation rules
│       │   ├── syntax-rules.yaml
│       │   ├── dependency-rules.yaml
│       │   ├── security-rules.yaml
│       │   └── best-practice-rules.yaml
│       └── schemas/                        # Validation schemas
│           └── validation-report.yaml
│
├── domain/                                   # Domain-specific expert agents
│   │
│   ├── packages/                            # Package selection & management
│   │   ├── agent.md                        # Agent definition
│   │   ├── strategies/                     # Package selection strategies
│   │   │   ├── minimal-strategy.md
│   │   │   ├── full-featured-strategy.md
│   │   │   └── custom-strategy-template.md
│   │   ├── catalogs/                       # Package categorization
│   │   │   ├── development-packages.yaml
│   │   │   ├── desktop-packages.yaml
│   │   │   ├── server-packages.yaml
│   │   │   ├── multimedia-packages.yaml
│   │   │   └── utility-packages.yaml
│   │   └── examples/                       # Example plans
│   │       ├── workstation-packages.yaml
│   │       ├── minimal-server-packages.yaml
│   │       └── gaming-packages.yaml
│   │
│   ├── services/                            # System services configuration
│   │   ├── agent.md                        # Agent definition
│   │   ├── service-types/                  # Service category templates
│   │   │   ├── web-servers.md
│   │   │   ├── databases.md
│   │   │   ├── containerization.md
│   │   │   ├── monitoring.md
│   │   │   └── networking.md
│   │   ├── templates/                      # Service configuration templates
│   │   │   ├── nginx-template.nix
│   │   │   ├── docker-template.nix
│   │   │   ├── postgresql-template.nix
│   │   │   └── prometheus-template.nix
│   │   └── examples/
│   │       ├── homelab-services.yaml
│   │       └── web-server-services.yaml
│   │
│   ├── hardware/                            # Hardware-specific configuration
│   │   ├── agent.md                        # Agent definition
│   │   ├── profiles/                       # Hardware profiles
│   │   │   ├── laptop-profiles/
│   │   │   │   ├── dell-xps.yaml
│   │   │   │   ├── lenovo-thinkpad.yaml
│   │   │   │   └── framework.yaml
│   │   │   ├── desktop-profiles/
│   │   │   │   ├── amd-desktop.yaml
│   │   │   │   └── intel-desktop.yaml
│   │   │   └── server-profiles/
│   │   │       └── generic-server.yaml
│   │   ├── drivers/                        # Driver recommendations
│   │   │   ├── gpu-drivers.yaml
│   │   │   ├── wifi-drivers.yaml
│   │   │   └── bluetooth-drivers.yaml
│   │   └── detection/                      # Hardware detection scripts
│   │       └── auto-detect.sh
│   │
│   ├── network/                             # Network configuration planning
│   │   ├── agent.md                        # Agent definition
│   │   ├── topologies/                     # Network topology patterns
│   │   │   ├── simple-home-network.yaml
│   │   │   ├── homelab-network.yaml
│   │   │   └── multi-vlan-network.yaml
│   │   ├── services/                       # Network service configs
│   │   │   ├── dns-config.md
│   │   │   ├── vpn-config.md
│   │   │   └── reverse-proxy-config.md
│   │   └── examples/
│   │       ├── workstation-network.yaml
│   │       └── server-network.yaml
│   │
│   ├── security/                            # Security & hardening planning
│   │   ├── agent.md                        # Agent definition
│   │   ├── policies/                       # Security policy templates
│   │   │   ├── basic-hardening.yaml
│   │   │   ├── moderate-hardening.yaml
│   │   │   ├── high-security.yaml
│   │   │   └── paranoid-security.yaml
│   │   ├── templates/                      # Security configuration templates
│   │   │   ├── firewall-template.nix
│   │   │   ├── apparmor-template.nix
│   │   │   └── fail2ban-template.nix
│   │   └── examples/
│   │       ├── workstation-security.yaml
│   │       └── server-security.yaml
│   │
│   ├── users/                               # User & group management planning
│   │   ├── agent.md                        # Agent definition
│   │   ├── personas/                       # User persona templates
│   │   │   ├── developer-persona.yaml
│   │   │   ├── admin-persona.yaml
│   │   │   ├── standard-user-persona.yaml
│   │   │   └── service-account-persona.yaml
│   │   ├── templates/                      # User configuration templates
│   │   │   └── user-config-template.nix
│   │   └── examples/
│   │       └── multi-user-setup.yaml
│   │
│   ├── desktop/                             # Desktop environment planning
│   │   ├── agent.md                        # Agent definition
│   │   ├── environments/                   # DE/WM configurations
│   │   │   ├── gnome/
│   │   │   │   ├── config.yaml
│   │   │   │   └── extensions.yaml
│   │   │   ├── kde/
│   │   │   │   └── config.yaml
│   │   │   ├── xfce/
│   │   │   │   └── config.yaml
│   │   │   ├── i3/
│   │   │   │   └── config.yaml
│   │   │   └── hyprland/
│   │   │       └── config.yaml
│   │   ├── themes/                         # Theme configurations
│   │   │   ├── dark-themes.yaml
│   │   │   └── light-themes.yaml
│   │   └── examples/
│   │       ├── gnome-workstation.yaml
│   │       └── i3-minimal.yaml
│   │
│   └── development/                         # Development environment planning
│       ├── agent.md                        # Agent definition
│       ├── stacks/                         # Technology stack templates
│       │   ├── web-development/
│       │   │   ├── frontend-stack.yaml
│       │   │   ├── backend-stack.yaml
│       │   │   └── fullstack-stack.yaml
│       │   ├── systems-programming/
│       │   │   ├── rust-stack.yaml
│       │   │   ├── cpp-stack.yaml
│       │   │   └── go-stack.yaml
│       │   ├── data-science/
│       │   │   └── python-ml-stack.yaml
│       │   └── mobile-development/
│       │       ├── android-stack.yaml
│       │       └── ios-stack.yaml
│       ├── tools/                          # Development tool configs
│       │   ├── editors.yaml
│       │   ├── version-control.yaml
│       │   └── containerization.yaml
│       └── examples/
│           ├── rust-developer.yaml
│           └── fullstack-developer.yaml
│
├── specialized/                             # Pre-configured specialized agents
│   │
│   ├── homelab/                            # Homelab server planning
│   │   ├── agent.md                        # Agent definition (combines multiple domain agents)
│   │   ├── presets/                        # Pre-configured homelab setups
│   │   │   ├── minimal-homelab.yaml
│   │   │   ├── media-server.yaml
│   │   │   ├── development-lab.yaml
│   │   │   └── full-homelab.yaml
│   │   └── examples/
│   │       └── complete-homelab.yaml
│   │
│   ├── workstation/                        # Developer workstation planning
│   │   ├── agent.md                        # Agent definition
│   │   ├── presets/                        # Pre-configured workstation types
│   │   │   ├── web-developer.yaml
│   │   │   ├── systems-programmer.yaml
│   │   │   ├── data-scientist.yaml
│   │   │   └── creative-professional.yaml
│   │   └── examples/
│   │       └── rust-workstation.yaml
│   │
│   ├── server/                             # Production server planning
│   │   ├── agent.md                        # Agent definition
│   │   ├── presets/                        # Server type presets
│   │   │   ├── web-server.yaml
│   │   │   ├── database-server.yaml
│   │   │   ├── application-server.yaml
│   │   │   └── container-host.yaml
│   │   └── examples/
│   │       └── production-web-server.yaml
│   │
│   └── minimal/                            # Minimal system planning
│       ├── agent.md                        # Agent definition
│       ├── presets/                        # Minimal configurations
│       │   ├── headless-minimal.yaml
│       │   ├── embedded-minimal.yaml
│       │   └── container-minimal.yaml
│       └── examples/
│           └── minimal-server.yaml
│
├── utilities/                               # Utility agents for special tasks
│   │
│   ├── analyzer/                           # Analyze existing configurations
│   │   ├── agent.md                        # Agent definition
│   │   ├── analyzers/                      # Different analysis types
│   │   │   ├── package-analyzer.md
│   │   │   ├── service-analyzer.md
│   │   │   ├── security-analyzer.md
│   │   │   └── performance-analyzer.md
│   │   └── examples/
│   │       └── analysis-report.yaml
│   │
│   ├── migrator/                           # Migration planning from other systems
│   │   ├── agent.md                        # Agent definition
│   │   ├── sources/                        # Migration source systems
│   │   │   ├── ubuntu-migration.md
│   │   │   ├── arch-migration.md
│   │   │   ├── fedora-migration.md
│   │   │   └── macos-migration.md
│   │   ├── strategies/                     # Migration strategies
│   │   │   ├── incremental-migration.md
│   │   │   └── full-migration.md
│   │   └── examples/
│   │       └── ubuntu-to-nixos.yaml
│   │
│   └── optimizer/                          # Configuration optimization
│       ├── agent.md                        # Agent definition
│       ├── optimizations/                  # Optimization strategies
│       │   ├── size-optimization.md
│       │   ├── performance-optimization.md
│       │   ├── security-optimization.md
│       │   └── maintainability-optimization.md
│       └── examples/
│           └── optimized-config.yaml
│
└── lib/                                     # Shared libraries & utilities
    │
    ├── agent-framework.md                  # Agent framework documentation
    ├── communication-protocol.md           # Inter-agent communication specs
    │
    ├── plan-schemas/                       # Standardized plan formats
    │   ├── base-plan.schema.yaml
    │   ├── package-plan.schema.yaml
    │   ├── service-plan.schema.yaml
    │   ├── hardware-plan.schema.yaml
    │   └── complete-plan.schema.yaml
    │
    ├── knowledge-base/                     # Shared NixOS knowledge
    │   │
    │   ├── nixos/                          # NixOS-specific knowledge
    │   │   ├── options-reference.md
    │   │   ├── module-system.md
    │   │   ├── best-practices.md
    │   │   ├── common-patterns.md
    │   │   └── troubleshooting.md
    │   │
    │   ├── hardware/                       # Hardware knowledge
    │   │   ├── cpu-vendors.md
    │   │   ├── gpu-vendors.md
    │   │   ├── device-drivers.md
    │   │   └── firmware.md
    │   │
    │   ├── software/                       # Software knowledge
    │   │   ├── package-ecosystems.md
    │   │   ├── service-patterns.md
    │   │   └── common-applications.md
    │   │
    │   └── security/                       # Security knowledge
    │       ├── hardening-techniques.md
    │       ├── common-vulnerabilities.md
    │       └── security-tools.md
    │
    ├── utilities/                          # Shared utility functions
    │   ├── plan-merger.md                  # How to merge plans
    │   ├── plan-validator.md               # How to validate plans
    │   ├── conflict-resolver.md            # How to resolve conflicts
    │   └── dependency-resolver.md          # How to resolve dependencies
    │
    └── templates/                          # Shared templates
        ├── nix-code-templates/
        │   ├── package-list.nix.template
        │   ├── service-config.nix.template
        │   └── module.nix.template
        └── documentation-templates/
            ├── decision-record.md.template
            └── implementation-guide.md.template
```

## Directory Creation Script

To quickly create this entire structure:

```bash
#!/usr/bin/env bash
# create-agent-structure.sh - Create the nixman agents directory structure

set -e

BASE_DIR="agents"

# Create directory function
create_dir() {
    mkdir -p "$BASE_DIR/$1"
    echo "Created: $BASE_DIR/$1"
}

# Create file function
create_file() {
    local file="$BASE_DIR/$1"
    mkdir -p "$(dirname "$file")"
    touch "$file"
    echo "Created: $file"
}

echo "Creating nixman agents directory structure..."

# Root level
create_file "README.md"

# Templates
create_file "templates/base-agent.template.md"
create_file "templates/planning-agent.template.md"
create_file "templates/integration-agent.template.md"
create_file "templates/specialized-agent.template.md"

# Core agents
create_file "core/architect/agent.md"
create_dir "core/architect/prompts"
create_dir "core/architect/schemas"
create_dir "core/architect/examples"

create_file "core/orchestrator/agent.md"
create_file "core/orchestrator/coordination.md"
create_dir "core/orchestrator/workflows"
create_file "core/orchestrator/agent-registry.yaml"
create_file "core/orchestrator/conflict-resolution.md"

create_file "core/validator/agent.md"
create_dir "core/validator/rules"
create_dir "core/validator/schemas"

# Domain agents
create_file "domain/packages/agent.md"
create_dir "domain/packages/strategies"
create_dir "domain/packages/catalogs"
create_dir "domain/packages/examples"

create_file "domain/services/agent.md"
create_dir "domain/services/service-types"
create_dir "domain/services/templates"
create_dir "domain/services/examples"

create_file "domain/hardware/agent.md"
create_dir "domain/hardware/profiles"
create_dir "domain/hardware/drivers"
create_dir "domain/hardware/detection"

create_file "domain/network/agent.md"
create_dir "domain/network/topologies"
create_dir "domain/network/services"
create_dir "domain/network/examples"

create_file "domain/security/agent.md"
create_dir "domain/security/policies"
create_dir "domain/security/templates"
create_dir "domain/security/examples"

create_file "domain/users/agent.md"
create_dir "domain/users/personas"
create_dir "domain/users/templates"
create_dir "domain/users/examples"

create_file "domain/desktop/agent.md"
create_dir "domain/desktop/environments"
create_dir "domain/desktop/themes"
create_dir "domain/desktop/examples"

create_file "domain/development/agent.md"
create_dir "domain/development/stacks"
create_dir "domain/development/tools"
create_dir "domain/development/examples"

# Specialized agents
create_file "specialized/homelab/agent.md"
create_dir "specialized/homelab/presets"
create_dir "specialized/homelab/examples"

create_file "specialized/workstation/agent.md"
create_dir "specialized/workstation/presets"
create_dir "specialized/workstation/examples"

create_file "specialized/server/agent.md"
create_dir "specialized/server/presets"
create_dir "specialized/server/examples"

create_file "specialized/minimal/agent.md"
create_dir "specialized/minimal/presets"
create_dir "specialized/minimal/examples"

# Utility agents
create_file "utilities/analyzer/agent.md"
create_dir "utilities/analyzer/analyzers"
create_dir "utilities/analyzer/examples"

create_file "utilities/migrator/agent.md"
create_dir "utilities/migrator/sources"
create_dir "utilities/migrator/strategies"
create_dir "utilities/migrator/examples"

create_file "utilities/optimizer/agent.md"
create_dir "utilities/optimizer/optimizations"
create_dir "utilities/optimizer/examples"

# Lib
create_file "lib/agent-framework.md"
create_file "lib/communication-protocol.md"
create_dir "lib/plan-schemas"
create_dir "lib/knowledge-base/nixos"
create_dir "lib/knowledge-base/hardware"
create_dir "lib/knowledge-base/software"
create_dir "lib/knowledge-base/security"
create_dir "lib/utilities"
create_dir "lib/templates/nix-code-templates"
create_dir "lib/templates/documentation-templates"

echo ""
echo "✓ Agent directory structure created successfully!"
echo ""
echo "Next steps:"
echo "1. Copy agent templates from root to templates/"
echo "2. Start filling in agent.md files using AGENT_TEMPLATE.md"
echo "3. Add knowledge base content to lib/knowledge-base/"
echo "4. Create example configurations"
```

## File Count Summary

```
Total directories: ~80
Total files: ~150+

Breakdown:
- Core agents: 3 agents (~15 files each)
- Domain agents: 8 agents (~10 files each)
- Specialized agents: 4 agents (~5 files each)
- Utility agents: 3 agents (~8 files each)
- Lib: ~30 shared files
- Templates: ~8 template files
```

## Priority Implementation Order

### Phase 1: Core Foundation (Start Here)
1. `lib/agent-framework.md` - Core framework docs
2. `lib/communication-protocol.md` - How agents talk
3. `templates/` - All template files
4. `core/orchestrator/` - Coordination system
5. `core/validator/` - Basic validation

### Phase 2: Essential Domain Agents
1. `domain/packages/` - Package selection (most used)
2. `domain/hardware/` - Hardware detection
3. `domain/services/` - Service configuration
4. `domain/security/` - Basic hardening

### Phase 3: Extended Domain Agents
1. `domain/desktop/` - Desktop environments
2. `domain/development/` - Dev environments
3. `domain/network/` - Networking
4. `domain/users/` - User management

### Phase 4: Specialized Agents
1. `specialized/workstation/` - Most common use case
2. `specialized/server/` - Server setups
3. `specialized/homelab/` - Homelab configurations
4. `specialized/minimal/` - Minimal systems

### Phase 5: Utility Agents
1. `utilities/analyzer/` - Analyze existing configs
2. `utilities/optimizer/` - Optimize configs
3. `utilities/migrator/` - Migration support

## Maintenance

### Adding a New Agent

1. Choose appropriate category (core/domain/specialized/utilities)
2. Create directory: `agents/<category>/<agent-name>/`
3. Copy template: `cp templates/planning-agent.template.md <category>/<agent-name>/agent.md`
4. Fill in agent definition
5. Add to orchestrator registry: `core/orchestrator/agent-registry.yaml`
6. Create examples: `<category>/<agent-name>/examples/`
7. Add tests (when test framework exists)

### Updating Structure

1. Update this document first
2. Update creation script
3. Add migration guide if breaking changes
4. Update dependent agents
5. Update orchestrator if coordination changes

---

**Legend:**
- `📁 directory/` - Directory
- `📄 file.md` - Markdown documentation
- `📋 file.yaml` - YAML configuration
- `💾 file.nix` - Nix configuration
- `🔧 file.sh` - Shell script
