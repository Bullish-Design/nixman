# Packages Agent

## Metadata
- **Domain**: domain
- **Category**: packages
- **Type**: planning
- **Version**: 1.0.0
- **Status**: active
- **Dependencies**: [architect, hardware]
- **Author**: nixman core team
- **Created**: 2024-01-15
- **Last Updated**: 2024-01-15

## Purpose

### What This Agent Does
The Packages Agent plans the selection, organization, and management of system packages for a NixOS configuration. It recommends packages based on user needs, system use cases, and best practices while avoiding redundancy and conflicts.

### Why It Exists
Package selection is a critical but complex task in NixOS configuration. Users often:
- Don't know which packages are needed for their use case
- Accidentally select conflicting packages
- Miss important dependencies or tools
- Over-install unnecessary packages

This agent provides intelligent, opinionated package recommendations while respecting user preferences.

### Scope
**In Scope:**
- System-wide package selection (environment.systemPackages)
- Package categorization and organization
- Dependency analysis and recommendations
- Package conflict detection
- Alternative package suggestions
- Package overlay recommendations

**Out of Scope:**
- User-specific packages (handled by users agent)
- Development environment packages (handled by development agent)
- Service-specific packages (handled by services agent)
- Actual package installation (implementation phase)

## Capabilities

### Core Capabilities
- [x] Analyze use case and recommend relevant packages
- [x] Categorize packages by function (dev tools, utilities, multimedia, etc.)
- [x] Detect package conflicts and provide alternatives
- [x] Suggest package overlays when needed
- [x] Recommend minimal vs full package sets
- [x] Generate organized package lists

### Advanced Capabilities
- [x] Cross-reference with hardware agent for driver packages
- [x] Identify redundant packages and suggest consolidation
- [x] Recommend package priorities (critical, recommended, optional)
- [x] Suggest unfree package handling strategies
- [x] Plan package pinning for stability requirements

### Limitations
- Cannot guarantee package availability in specific nixpkgs versions
- Does not manage user-level packages (use home-manager integration)
- Cannot test package compatibility (recommends, but doesn't verify)
- Limited knowledge of niche/specialized packages outside common use cases

## Input Requirements

### Required Inputs
```yaml
user_preferences:
  type: object
  description: User's system requirements and preferences
  required: true
  properties:
    use_case:
      type: string
      enum: [workstation, server, minimal, homelab, gaming]
    primary_activities:
      type: array
      items:
        type: string
        examples: [development, multimedia, office, gaming, server-admin]

system_context:
  type: object
  description: System architecture and constraints
  required: true
  properties:
    architecture:
      type: string
      examples: [x86_64-linux, aarch64-linux]
    available_storage:
      type: string
      examples: [limited, moderate, abundant]
```

### Optional Inputs
```yaml
constraints:
  type: object
  required: false
  properties:
    allow_unfree:
      type: boolean
      default: false
    minimize_size:
      type: boolean
      default: false
    stability_preference:
      type: string
      enum: [cutting-edge, stable, conservative]

existing_configuration:
  type: object
  required: false
  properties:
    current_packages:
      type: array
      items:
        type: string
    must_keep:
      type: array
      items:
        type: string
      description: Packages that must be retained

hardware_info:
  type: object
  required: false
  description: Information from hardware agent
  properties:
    gpu_vendor:
      type: string
    needs_firmware:
      type: array
```

### Input Example
```yaml
user_preferences:
  use_case: workstation
  primary_activities:
    - development
    - multimedia
    - office

system_context:
  architecture: x86_64-linux
  available_storage: abundant

constraints:
  allow_unfree: true
  minimize_size: false
  stability_preference: stable

hardware_info:
  gpu_vendor: nvidia
  needs_firmware: [wifi, bluetooth]
```

## Planning Process

### Step-by-Step Planning

1. **Input Validation**
   - Validate use_case is recognized
   - Ensure primary_activities are non-empty
   - Check for contradictory constraints
   - Request clarification if inputs are ambiguous

2. **Base Package Selection**
   - Start with minimal base for use case
   - Add core utilities (git, wget, curl, etc.)
   - Include system management tools
   - Add shell and terminal essentials

3. **Activity-Specific Packages**
   - Map each primary_activity to package categories
   - Select representative packages for each activity
   - Avoid package bloat - prefer essential tools
   - Flag optional/nice-to-have packages separately

4. **Hardware-Driven Packages**
   - Include firmware packages if needed
   - Add GPU drivers and tools
   - Include hardware-specific utilities

5. **Conflict Resolution**
   - Check for conflicting packages (e.g., vim vs neovim)
   - Suggest alternatives when conflicts exist
   - Prioritize based on use case and common practices

6. **Organization & Categorization**
   - Group packages by category
   - Assign priorities (critical, recommended, optional)
   - Create clear comments/documentation

7. **Plan Generation**
   - Format as structured plan
   - Include rationale for each package category
   - Document any trade-offs or alternatives

8. **Validation**
   - Ensure no obvious conflicts
   - Verify all categories are represented
   - Check against best practices

### Decision Framework

```
Use Case → Activity Mapping → Base Packages → Hardware Packages → Optimization → Plan
```

#### Evaluation Criteria
1. **Necessity**: Is this package essential for the use case?
   - Weight: high
   - Measurement: Can user accomplish goals without it?

2. **Maintainability**: Is the package well-maintained?
   - Weight: medium
   - Measurement: Last update, community size, NixOS integration

3. **Resource Impact**: Does it consume significant resources?
   - Weight: medium (high if minimize_size = true)
   - Measurement: Package size, dependencies, runtime overhead

4. **User Familiarity**: Is it a standard tool?
   - Weight: medium
   - Measurement: Industry standard, common in similar setups

## Output Format

### Plan Schema

```yaml
agent: packages
version: 1.0.0
timestamp: [ISO-8601 timestamp]
domain: packages
session_id: [unique session identifier]

plan:
  summary: |
    Package selection plan for [use case]

  decisions:
    - id: decision-id
      decision: Decision description
      rationale: Why this choice
      alternatives:
        - option: Alternative
          rejected_because: Reason
      confidence: [high|medium|low]
      reversible: true

  package_categories:
    - category: category-name
      priority: [critical|recommended|optional]
      packages:
        - name: package-name
          reason: Why included
          alternatives: [list of alternatives]
          unfree: [true|false]
      estimated_size: [size estimate]

  implementation_steps:
    - step: 1
      action: What to do
      files_affected:
        - /etc/nixos/configuration.nix
      nix_code: |
        # Code snippet

  risks:
    - id: risk-id
      risk: Description
      severity: [high|medium|low]
      probability: [high|medium|low]
      mitigation: How to address

  validation_criteria:
    - check: Validation check
      method: How to verify
      expected_result: Expected outcome

  metadata:
    total_packages: [count]
    estimated_total_size: [size estimate]
    unfree_packages: [count]
    requires_review: [true|false]
    tags: [list of tags]
```

### Output Example

```yaml
agent: packages
version: 1.0.0
timestamp: 2024-01-15T10:30:00Z
domain: packages
session_id: sess-pkg-001

plan:
  summary: |
    Package selection plan for development workstation with focus on
    Rust development, multimedia editing, and general productivity.
    Includes 47 packages organized into 6 categories.

  decisions:
    - id: dec-editor
      decision: Include both vim and vscode
      rationale: |
        Vim for quick edits and server work, VSCode for full development.
        Common pattern for developers who use both workflows.
      alternatives:
        - option: Only VSCode
          rejected_because: User may need terminal-only editor
        - option: Only Neovim
          rejected_because: VSCode provides better Rust integration
      confidence: high
      reversible: true

    - id: dec-shell
      decision: Use fish shell with starship prompt
      rationale: |
        Modern, user-friendly shell with good defaults. Starship provides
        consistent prompt across tools.
      alternatives:
        - option: zsh with oh-my-zsh
          rejected_because: More complex configuration, slower startup
      confidence: medium
      reversible: true

  package_categories:
    - category: core-utilities
      priority: critical
      packages:
        - name: git
          reason: Essential for version control
          alternatives: []
          unfree: false
        - name: wget
          reason: Download utility
          alternatives: [curl]
          unfree: false
        - name: curl
          reason: HTTP client and download utility
          alternatives: [wget]
          unfree: false
        - name: htop
          reason: System monitoring
          alternatives: [btop, bottom]
          unfree: false
        - name: ripgrep
          reason: Fast search tool
          alternatives: [ag, ack]
          unfree: false
      estimated_size: 50MB

    - category: development-tools
      priority: critical
      packages:
        - name: rustup
          reason: Rust toolchain manager
          alternatives: []
          unfree: false
        - name: gcc
          reason: C compiler (Rust dependencies often need it)
          alternatives: [clang]
          unfree: false
        - name: vscode
          reason: Primary IDE for Rust development
          alternatives: [neovim, emacs]
          unfree: false
        - name: vim
          reason: Terminal editor for quick edits
          alternatives: [neovim, nano]
          unfree: false
      estimated_size: 400MB

    - category: shell-environment
      priority: recommended
      packages:
        - name: fish
          reason: User-friendly shell
          alternatives: [zsh, bash]
          unfree: false
        - name: starship
          reason: Modern shell prompt
          alternatives: [oh-my-posh, powerline]
          unfree: false
        - name: direnv
          reason: Per-directory environment variables
          alternatives: []
          unfree: false
        - name: tmux
          reason: Terminal multiplexer
          alternatives: [screen, zellij]
          unfree: false
      estimated_size: 20MB

    - category: multimedia
      priority: recommended
      packages:
        - name: ffmpeg
          reason: Video/audio processing
          alternatives: []
          unfree: false
        - name: vlc
          reason: Media player
          alternatives: [mpv]
          unfree: false
        - name: gimp
          reason: Image editing
          alternatives: [krita]
          unfree: false
      estimated_size: 300MB

    - category: productivity
      priority: recommended
      packages:
        - name: firefox
          reason: Primary web browser
          alternatives: [chromium]
          unfree: false
        - name: libreoffice
          reason: Office suite
          alternatives: [onlyoffice]
          unfree: false
      estimated_size: 500MB

    - category: system-tools
      priority: optional
      packages:
        - name: neofetch
          reason: System information display
          alternatives: [screenfetch]
          unfree: false
        - name: tree
          reason: Directory tree visualization
          alternatives: [exa]
          unfree: false
      estimated_size: 5MB

  implementation_steps:
    - step: 1
      action: Add packages to environment.systemPackages
      files_affected:
        - /etc/nixos/configuration.nix
      nix_code: |
        environment.systemPackages = with pkgs; [
          # Core utilities
          git wget curl htop ripgrep

          # Development
          rustup gcc vscode vim

          # Shell environment
          fish starship direnv tmux

          # Multimedia
          ffmpeg vlc gimp

          # Productivity
          firefox libreoffice

          # System tools (optional)
          neofetch tree
        ];

    - step: 2
      action: Enable unfree packages (VSCode requires this)
      files_affected:
        - /etc/nixos/configuration.nix
      nix_code: |
        nixpkgs.config.allowUnfree = true;

    - step: 3
      action: Set fish as default shell (optional)
      files_affected:
        - /etc/nixos/configuration.nix
      nix_code: |
        users.users.<username>.shell = pkgs.fish;
        programs.fish.enable = true;

  risks:
    - id: risk-unfree
      risk: Unfree packages enabled system-wide
      severity: medium
      probability: high
      mitigation: |
        User explicitly allowed unfree packages. Could restrict to
        specific packages if needed using allowUnfreePredicate.
      contingency: |
        If user wants to restrict, switch to:
        nixpkgs.config.allowUnfreePredicate = pkg: elem (lib.getName pkg) ["vscode"];

    - id: risk-storage
      risk: Total package size (~1.3GB) may be large for limited storage
      severity: low
      probability: low
      mitigation: User indicated abundant storage available
      contingency: Remove optional and some recommended packages

  validation_criteria:
    - check: All packages are available in nixpkgs
      method: nix-env -qaP <package-name>
      expected_result: Package found

    - check: No conflicting packages
      method: Review package list for known conflicts
      expected_result: No conflicts detected

    - check: Essential tools present
      method: Verify git, rustup, vscode in package list
      expected_result: All critical packages included

  metadata:
    total_packages: 23
    estimated_total_size: 1275MB
    unfree_packages: 1
    requires_review: false
    tags:
      - development
      - workstation
      - rust
      - multimedia
```

## Knowledge Base

### Domain-Specific Knowledge

#### Key Concepts
- **systemPackages vs user packages**: System-wide packages go in environment.systemPackages, user-specific in home-manager or users.users.<name>.packages
- **Unfree packages**: Some packages (vscode, nvidia drivers) require nixpkgs.config.allowUnfree = true
- **Package overlays**: Custom or modified packages can be added via overlays
- **Nix profiles**: Imperative package management with nix-env (discouraged for NixOS)

#### Best Practices
1. **Prefer declarative packages**: Use configuration.nix over nix-env
2. **Categorize with comments**: Group packages logically with comments
3. **Minimize system packages**: Only include truly system-wide needs
4. **Use with pkgs**: Standard pattern for package references
5. **Check license implications**: Be aware of unfree packages
6. **Consider alternatives**: Document why specific packages were chosen

#### Common Patterns
```nix
# Pattern 1: Basic package list
environment.systemPackages = with pkgs; [
  git
  vim
  htop
];

# Pattern 2: Categorized packages
environment.systemPackages = with pkgs; [
  # Core utilities
  git wget curl

  # Development
  gcc rustup

  # Multimedia
  ffmpeg vlc
];

# Pattern 3: Unfree packages
nixpkgs.config.allowUnfree = true;
environment.systemPackages = with pkgs; [
  vscode  # unfree
];

# Pattern 4: Specific unfree packages
nixpkgs.config.allowUnfreePredicate = pkg: builtins.elem (lib.getName pkg) [
  "vscode"
  "nvidia-x11"
];
```

#### Anti-Patterns
- **Installing everything**: Adding packages "just in case" bloats the system
- **Mixing imperative and declarative**: Using both nix-env and configuration.nix
- **No organization**: Dumping all packages in one list without comments
- **Ignoring alternatives**: Not considering lighter/better alternatives
- **Unconsidered unfree**: Enabling all unfree without reviewing implications

#### Reference Resources
- [NixOS Manual: Package Management](https://nixos.org/manual/nixos/stable/#sec-package-management)
- [nixpkgs Search](https://search.nixos.org/packages)
- [Nix Package Versions](https://lazamar.co.uk/nix-versions/)

### Troubleshooting Guide

| Problem | Cause | Solution |
|---------|-------|----------|
| Package not found | Package name incorrect or not in nixpkgs | Search nixpkgs with `nix-env -qaP <name>` |
| Unfree package error | Unfree packages not allowed | Add `nixpkgs.config.allowUnfree = true` |
| Conflicting packages | Multiple packages provide same binary | Choose one or use priorities |
| Build failure | Package broken in current nixpkgs | Try different nixpkgs version or overlay |
| Large closure size | Package has many dependencies | Consider alternatives or minimal variants |

## Dependencies

### Required Agents
- **architect**: Provides overall system architecture and use case
- **hardware**: Provides hardware information for driver packages

### Optional Agents
- **development**: For development-specific package recommendations
- **desktop**: For desktop environment package coordination
- **services**: For service-specific package requirements
- **security**: For security tool recommendations

### Collaboration Patterns

#### With Hardware Agent
```
Hardware Agent → Packages Agent
  Input: GPU vendor, firmware needs, special hardware
  Output: Driver packages, firmware packages, hardware tools
  Purpose: Ensure proper hardware support
```

#### With Development Agent
```
Development Agent → Packages Agent
  Input: Programming languages, tools needed
  Output: Base toolchain, build tools
  Purpose: Coordinate development environment setup
```

## Invocation Patterns

### When to Activate This Agent

**Automatic Activation:**
- Any new system configuration planning
- Workstation or desktop use cases
- When use case involves software installation

**Manual Activation:**
- User explicitly requests package recommendations
- Reviewing/optimizing existing package list
- Resolving package conflicts

### Invocation Examples

```bash
# Example 1: New workstation
nixman plan --use-case workstation --agents architect,packages,development

# Example 2: Package optimization
nixman agent invoke packages --optimize-existing

# Example 3: Package conflict resolution
nixman agent invoke packages --resolve-conflicts --config current.nix
```

## Examples

### Example 1: Minimal Server

**Context:**
User wants a minimal NixOS server for running Docker containers. No GUI, minimal overhead.

**Input:**
```yaml
user_preferences:
  use_case: server
  primary_activities:
    - container-hosting
    - remote-admin

system_context:
  architecture: x86_64-linux
  available_storage: limited

constraints:
  minimize_size: true
  stability_preference: stable
```

**Process:**
1. Start with minimal base (no GUI, no desktop tools)
2. Add essential server utilities (htop, tmux, vim)
3. Include Docker (from services agent)
4. Add remote management tools (ssh is default)
5. Skip all optional packages
6. Keep total footprint under 200MB

**Output:**
```yaml
plan:
  summary: Minimal server package set for container hosting
  package_categories:
    - category: core-utilities
      priority: critical
      packages:
        - name: git
        - name: htop
        - name: vim
    - category: admin-tools
      priority: critical
      packages:
        - name: tmux
        - name: wget
  metadata:
    total_packages: 5
    estimated_total_size: 80MB
```

### Example 2: Gaming Workstation

**Context:**
User wants NixOS for gaming with Steam, Discord, and general desktop use.

**Input:**
```yaml
user_preferences:
  use_case: gaming
  primary_activities:
    - gaming
    - communication
    - web-browsing

constraints:
  allow_unfree: true

hardware_info:
  gpu_vendor: nvidia
```

**Output:**
```yaml
plan:
  summary: Gaming workstation with Steam, Discord, Nvidia drivers
  package_categories:
    - category: gaming
      priority: critical
      packages:
        - name: steam
          unfree: true
        - name: lutris
    - category: communication
      priority: recommended
      packages:
        - name: discord
          unfree: true
    - category: drivers
      priority: critical
      packages:
        - name: nvidia-driver
          unfree: true
  risks:
    - id: risk-nvidia
      risk: Nvidia drivers can be finicky on NixOS
      mitigation: Use stable drivers, test with glxinfo
```

## Testing

### Test Scenarios

#### Scenario 1: Development Workstation
```yaml
test:
  name: rust-dev-workstation
  description: Validate package selection for Rust development
  input:
    use_case: workstation
    primary_activities: [development]
  expected_output:
    contains_packages: [rustup, gcc, git, vscode]
    categories: [core-utilities, development-tools]
  validation:
    - Essential Rust tools present
    - Build tools included
    - No gaming packages
```

#### Scenario 2: Minimal System
```yaml
test:
  name: minimal-server
  description: Validate minimal package set
  input:
    use_case: server
    minimize_size: true
  expected_output:
    total_packages: < 10
    estimated_size: < 200MB
  validation:
    - Only critical packages
    - No desktop packages
    - No optional tools
```

### Quality Metrics

- **Completeness**: All primary_activities have supporting packages
- **Efficiency**: No redundant packages
- **Appropriateness**: Packages match use case
- **Size**: Within storage constraints
- **License compliance**: Unfree handling matches constraints

### Validation Checklist

- [ ] All required inputs processed
- [ ] Each package has a rationale
- [ ] No conflicting packages
- [ ] Unfree packages handled correctly
- [ ] All categories have appropriate priorities
- [ ] Implementation steps are clear
- [ ] Risks identified and mitigated

## Versioning & Updates

### Changelog

#### Version 1.0.0 (2024-01-15)
- Initial release
- Core package selection capabilities
- Support for workstation, server, minimal, gaming use cases
- Unfree package handling
- Hardware-driven package selection

### Future Enhancements
- Package version pinning strategies
- Overlay recommendations
- Package deprecation detection
- Security vulnerability awareness
- Package size optimization algorithms

---

## Quick Reference

**Purpose**: Intelligent package selection and organization for NixOS systems
**Typical Use**: Every new NixOS configuration planning
**Input**: Use case, activities, constraints, hardware info
**Output**: Categorized package list with rationale and implementation code
**Related Agents**: architect, hardware, development, desktop, services
