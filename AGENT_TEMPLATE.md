# Agent Template for nixman

This is a base template for creating new planning agents in the nixman system.

---

# [Agent Name] Agent

## Metadata
- **Domain**: [core|domain|specialized|utility]
- **Category**: [specific category, e.g., "packages", "services", "hardware"]
- **Type**: [planning|analysis|integration|validation]
- **Version**: 1.0.0
- **Status**: [draft|active|deprecated]
- **Dependencies**: [list of other agents this depends on]
- **Author**: [Your name or team]
- **Created**: [Date]
- **Last Updated**: [Date]

## Purpose

### What This Agent Does
[2-3 sentence description of the agent's primary purpose]

### Why It Exists
[Explanation of the problem this agent solves]

### Scope
**In Scope:**
- [What this agent handles]
- [Specific responsibilities]

**Out of Scope:**
- [What this agent does NOT handle]
- [Responsibilities of other agents]

## Capabilities

### Core Capabilities
- [ ] [Capability 1: e.g., "Analyze hardware specifications"]
- [ ] [Capability 2: e.g., "Generate hardware-optimized configurations"]
- [ ] [Capability 3: e.g., "Detect driver requirements"]

### Advanced Capabilities
- [ ] [Advanced capability 1]
- [ ] [Advanced capability 2]

### Limitations
- [Known limitation 1]
- [Known limitation 2]

## Input Requirements

### Required Inputs
```yaml
# Inputs that MUST be provided
user_preferences:
  type: object
  description: User's preferences and requirements
  required: true

system_context:
  type: object
  description: Current system state or target environment
  required: true
```

### Optional Inputs
```yaml
# Inputs that enhance planning but aren't required
constraints:
  type: object
  description: Any constraints to consider
  required: false

existing_configuration:
  type: object
  description: Existing config to build upon
  required: false
```

### Input Example
```yaml
user_preferences:
  use_case: "development workstation"
  primary_language: "rust"

system_context:
  hardware:
    cpu: "AMD Ryzen 9"
    ram: "32GB"
```

## Planning Process

### Step-by-Step Planning

1. **Input Validation**
   - Validate required inputs are present
   - Check input format and constraints
   - Request clarification if needed

2. **Analysis**
   - [What the agent analyzes]
   - [How it processes information]
   - [Decision-making criteria]

3. **Decision Making**
   - [How decisions are made]
   - [What factors are considered]
   - [Trade-off evaluation]

4. **Plan Generation**
   - [How the plan is structured]
   - [What components are included]
   - [Format and schema]

5. **Validation**
   - [Self-validation steps]
   - [Consistency checks]
   - [Quality assurance]

### Decision Framework

```
Input → Analysis → Options Generation → Evaluation → Selection → Plan
```

#### Evaluation Criteria
1. **Criterion 1**: [e.g., "Performance impact"]
   - Weight: [high|medium|low]
   - Measurement: [how it's measured]

2. **Criterion 2**: [e.g., "Maintainability"]
   - Weight: [high|medium|low]
   - Measurement: [how it's measured]

## Output Format

### Plan Schema

```yaml
agent: [agent-name]
version: 1.0.0
timestamp: [ISO-8601 timestamp]
domain: [domain-name]
session_id: [unique session identifier]

plan:
  summary: |
    Brief summary of the plan (2-3 sentences)

  decisions:
    - id: decision-1
      decision: What was decided
      rationale: Why this decision was made
      alternatives:
        - option: Alternative option
          rejected_because: Why it wasn't chosen
      confidence: [high|medium|low]
      reversible: [true|false]

  components:
    - id: component-1
      name: Component name
      type: Component type
      priority: [critical|high|medium|low]
      configuration:
        # Component-specific configuration
      dependencies:
        - component-id
        - external-dependency
      estimated_complexity: [simple|moderate|complex]

  implementation_steps:
    - step: 1
      action: What to do
      files_affected:
        - file/path.nix
      dependencies:
        - component-id
      validation: How to verify this step

  risks:
    - id: risk-1
      risk: Potential issue
      severity: [high|medium|low]
      probability: [high|medium|low]
      mitigation: How to address
      contingency: Backup plan

  validation_criteria:
    - check: What to validate
      method: How to validate
      expected_result: What success looks like

  metadata:
    estimated_complexity: [simple|moderate|complex]
    requires_review: [true|false]
    tags:
      - tag1
      - tag2
```

### Output Example

```yaml
agent: example-agent
version: 1.0.0
timestamp: 2024-01-15T10:30:00Z
domain: example
session_id: sess-abc123

plan:
  summary: |
    This plan configures example components for a development
    environment with focus on performance and maintainability.

  decisions:
    - id: dec-1
      decision: Use example tool A instead of B
      rationale: Better integration with NixOS module system
      alternatives:
        - option: Tool B
          rejected_because: Requires additional system dependencies
      confidence: high
      reversible: true

  components:
    - id: comp-1
      name: Example Component
      type: service
      priority: high
      configuration:
        enable: true
        setting1: value1
      dependencies:
        - nixpkgs.example-package
      estimated_complexity: moderate

  implementation_steps:
    - step: 1
      action: Add example package to system packages
      files_affected:
        - /etc/nixos/configuration.nix
      dependencies: []
      validation: Run 'which example-command'

  risks:
    - id: risk-1
      risk: Configuration might conflict with existing setup
      severity: medium
      probability: low
      mitigation: Validate before applying
      contingency: Rollback using NixOS generations

  validation_criteria:
    - check: Example service is running
      method: systemctl status example.service
      expected_result: Active (running)

  metadata:
    estimated_complexity: moderate
    requires_review: false
    tags:
      - development
      - example
```

## Knowledge Base

### Domain-Specific Knowledge

#### Key Concepts
- **Concept 1**: [Explanation]
- **Concept 2**: [Explanation]

#### Best Practices
1. [Best practice 1]
2. [Best practice 2]
3. [Best practice 3]

#### Common Patterns
```nix
# Pattern 1: [Description]
{
  # Example NixOS configuration
}
```

#### Anti-Patterns
- **Anti-pattern 1**: [What to avoid and why]
- **Anti-pattern 2**: [What to avoid and why]

#### Reference Resources
- [NixOS Manual: Relevant Section](URL)
- [nixpkgs Documentation: Relevant Section](URL)
- [Community Resources](URL)

### Troubleshooting Guide

| Problem | Cause | Solution |
|---------|-------|----------|
| Issue 1 | Root cause | How to fix |
| Issue 2 | Root cause | How to fix |

## Dependencies

### Required Agents
- **[Agent Name]**: Why this dependency exists
- **[Agent Name]**: Why this dependency exists

### Optional Agents
- **[Agent Name]**: When this is useful
- **[Agent Name]**: When this is useful

### Collaboration Patterns

#### With [Other Agent]
```
This Agent → [Other Agent]
  Input: [What is sent]
  Output: [What is received]
  Purpose: [Why they collaborate]
```

## Invocation Patterns

### When to Activate This Agent

**Automatic Activation:**
- [Scenario 1 that triggers this agent]
- [Scenario 2 that triggers this agent]

**Manual Activation:**
- [When user should explicitly request this agent]
- [When user should explicitly request this agent]

### Invocation Examples

```bash
# Example 1: Direct invocation
nixman agent invoke [agent-name] --input input.yaml

# Example 2: As part of workflow
nixman plan --agents "architect,[agent-name],validator"

# Example 3: With specific parameters
nixman agent invoke [agent-name] --param key=value
```

## Examples

### Example 1: [Scenario Name]

**Context:**
[Describe the scenario]

**Input:**
```yaml
# Example input
```

**Process:**
1. [What the agent does first]
2. [What the agent does next]
3. [Final steps]

**Output:**
```yaml
# Example output (abbreviated)
plan:
  summary: |
    [Summary of generated plan]
  components:
    - name: example-component
      type: example-type
```

**Explanation:**
[Why the agent made these decisions]

### Example 2: [Another Scenario]

[Follow same format as Example 1]

## Testing

### Test Scenarios

#### Scenario 1: [Test Name]
```yaml
test:
  name: [test-name]
  description: What this test validates
  input:
    # Test input
  expected_output:
    # Expected plan characteristics
  validation:
    - Check 1
    - Check 2
```

### Quality Metrics

- **Completeness**: All required components addressed
- **Consistency**: No conflicting configurations
- **Feasibility**: Plan is implementable
- **Best Practices**: Follows NixOS conventions
- **Documentation**: Clear decision rationale

### Validation Checklist

- [ ] All required inputs processed
- [ ] All decisions have rationale
- [ ] All components have dependencies resolved
- [ ] All risks have mitigations
- [ ] Output matches schema
- [ ] Plan is self-consistent
- [ ] Best practices followed

## Versioning & Updates

### Changelog

#### Version 1.0.0 (YYYY-MM-DD)
- Initial release
- Core capabilities: [list]

#### Version 1.1.0 (YYYY-MM-DD)
- Added: [new feature]
- Fixed: [bug fix]
- Changed: [breaking change]

### Upgrade Notes

When upgrading from previous versions:
- [Migration note 1]
- [Migration note 2]

## Contributing

### How to Improve This Agent

1. [How to add new capabilities]
2. [How to extend knowledge base]
3. [How to improve planning logic]

### Feedback

- Issue tracker: [URL or location]
- Discussion: [Where to discuss improvements]

---

## Quick Reference

**Purpose**: [One-line description]
**Typical Use**: [Common use case]
**Input**: [Key inputs needed]
**Output**: [What it produces]
**Related Agents**: [List of related agents]

---

## Template Notes

When using this template:

1. **Replace all [placeholders]** with actual content
2. **Remove sections** that don't apply to your agent
3. **Add sections** specific to your agent's needs
4. **Include concrete examples** - the more specific, the better
5. **Keep it updated** as the agent evolves
6. **Write for humans** - clear, concise, practical

The goal is to make it easy for:
- Users to understand when and how to use this agent
- Developers to extend and improve this agent
- Other agents to collaborate with this agent
- The orchestrator to effectively coordinate this agent
