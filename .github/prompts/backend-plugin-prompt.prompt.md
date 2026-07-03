---
mode: agent
agent: backend-plugin
name: backend-plugin-prompt
description: "Prompt for the backend-plugin agent. Creates and updates plugin components including skills, hooks, rules, and agent definitions in the plugin/ directory."
---

### Requirements

1. **Skill Structure:** Each skill lives in `plugin/skills/<name>/SKILL.md` with frontmatter (name, description) followed by focus areas, goals, output format, and workflow steps.
2. **Hook Format:** Hooks are JSON files in `plugin/hooks/` following the existing pattern (ai-guardrails.json, event-streaming.json, etc.). Each hook has an id, name, event, and action.
3. **Plugin Manifest:** The root `plugin/.plugin/plugin.json` declares supported features (agents, skills, rules, hooks), discovery settings, and orchestration config. Update it when adding new plugin types.
4. **Skill Discovery:** Skills are auto-discovered from `plugin/skills/` by the router. Each skill directory must contain a `SKILL.md` with a descriptive `name` field in the frontmatter.

### Constraints

- SKILL.md frontmatter must include `name` and `description`
- Hook JSON must include `id`, `name`, `event`, and `action` fields
- Follow existing 18 skills for naming and description conventions
- Plugin agent definitions go in `plugin/agents/`, not `.github/agents/`

### Success Criteria

- Skill appears in the plugin catalog when `discover_all()` runs
- Hook triggers on the specified event
- Rule enforces without errors
- `plugin.json` validates against the schema

### Usage Template

```
Create/update a plugin component:
- Type: [skill/hook/rule/agent]
- Name: [component name]
- Description: [brief description]
- Event/Action: [for hooks — trigger and command]
Show the diff and wait for my confirmation before applying.
```

### Chat Example

```
User: Create a new discover-cron-scheduler skill under plugin/skills/ that lists all scheduled task configurations in the project.
```

Agent (expected):
- Creates `plugin/skills/discover-cron-scheduler/SKILL.md` with frontmatter and workflow
- Follows the pattern from existing skills like discover-database-config
- Shows diff and waits for confirmation
