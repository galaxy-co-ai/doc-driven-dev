# 02 - User Personas

<!-- AI: This document defines WHO we're building for. Complete this after doc 01 (Vision and Goals) and before doc 03 (Product Requirements). Good personas lead to good requirements. -->

## Persona Research Methods

<!-- AI:
Before creating personas, gather real data. Methods include:
- User interviews (5-10 conversations with target users)
- Support ticket analysis (what do users struggle with?)
- Analytics data (how do current users behave?)
- Competitor reviews (what do users love/hate about alternatives?)
- Social media/forums (where do they discuss this problem?)

If no real data is available, document assumptions and plan to validate.
-->

| Method | Completed | Key Insights |
|--------|-----------|--------------|
| User interviews | <!-- AI: Yes/No/Planned --> | <!-- AI: Key findings --> |
| Support ticket analysis | <!-- AI: Yes/No/N/A --> | <!-- AI: Key findings --> |
| Competitor review analysis | <!-- AI: Yes/No/Planned --> | <!-- AI: Key findings --> |
| Other: <!-- AI: method --> | <!-- AI: Yes/No --> | <!-- AI: Key findings --> |

---

## Primary Persona

<!-- AI:
The primary persona is the user you're primarily designing for. All MVP features should serve this persona. When in doubt about a feature decision, ask "Would [Primary Persona Name] need this?"

Make the persona specific and memorable. Use a real name, specific job title, and concrete details. Avoid generic descriptions.
-->

### Profile

<!-- AI:
Create a believable person. Include:
- Name: A realistic name makes the persona memorable
- Role/Job Title: Be specific (not "developer" but "frontend developer at a startup")
- Company Size: Solo, small team (2-10), mid-size (10-100), enterprise (100+)
- Technical Level: Novice, intermediate, expert (in relevant domain)
- Demographics: Age range, location if relevant
-->

| Attribute | Value |
|-----------|-------|
| **Name** | <!-- AI: e.g., "Alex Chen" --> |
| **Role** | <!-- AI: e.g., "Senior Frontend Developer at a fintech startup" --> |
| **Company Size** | <!-- AI: e.g., "Team of 8" --> |
| **Technical Level** | <!-- AI: e.g., "Expert in React, intermediate in backend" --> |
| **Primary Goal** | <!-- AI: e.g., "Ship features faster without sacrificing quality" --> |

### Background

<!-- AI:
2-3 sentences describing their work context and how they encountered this problem. This helps empathize with their situation.
-->

<!-- AI: e.g., "Alex leads frontend development at a fast-growing fintech startup. They're responsible for building the customer-facing dashboard but spend too much time on repetitive tasks that could be automated. They've tried several tools but none fit their specific workflow." -->

### Pain Points (Current State)

<!-- AI:
List 3-5 specific frustrations this persona has TODAY (before using your product).
Each pain point should be:
- Specific (not "it's hard" but "takes 2 hours every week")
- Observable (something you could see them struggle with)
- Consequential (causes real problems: wasted time, lost money, frustration)
-->

| Pain Point | Impact | Frequency |
|------------|--------|-----------|
| <!-- AI: e.g., "Manually updating documentation after API changes" --> | <!-- AI: e.g., "2 hours wasted per sprint" --> | <!-- AI: e.g., "Every sprint" --> |
| <!-- AI: e.g., "Context-switching between 5+ browser tabs" --> | <!-- AI: e.g., "Breaks focus, slows development" --> | <!-- AI: e.g., "Daily" --> |
| <!-- AI: e.g., "Debugging integration issues without proper logs" --> | <!-- AI: e.g., "Hours lost on preventable bugs" --> | <!-- AI: e.g., "Weekly" --> |

### Use Cases

<!-- AI:
Define the specific tasks this persona will accomplish with your product.
For each use case, include:
- Trigger: What prompts this action?
- Action: What do they do?
- Outcome: What does success look like?
- Frequency: How often does this happen?

Frequency guide:
- Critical (multiple times/day) - Must be extremely fast and frictionless
- Daily - Should be quick and easy
- Weekly - Can have some complexity if valuable
- Monthly - Can require more steps if outcome is significant
- Rare - Focus on clarity over speed
-->

| Use Case | Trigger | Expected Outcome | Frequency |
|----------|---------|------------------|-----------|
| <!-- AI: e.g., "Quick lookup" --> | <!-- AI: e.g., "Needs API reference while coding" --> | <!-- AI: e.g., "Finds answer in < 30 seconds" --> | <!-- AI: e.g., "Critical (10+/day)" --> |
| <!-- AI: e.g., "Project setup" --> | <!-- AI: e.g., "Starting new project" --> | <!-- AI: e.g., "Boilerplate ready in < 5 min" --> | <!-- AI: e.g., "Weekly" --> |
| <!-- AI: e.g., "Debugging" --> | <!-- AI: e.g., "Encountering an error" --> | <!-- AI: e.g., "Root cause identified in < 10 min" --> | <!-- AI: e.g., "Daily" --> |

### Workflow Expectations

<!-- AI:
Describe how this persona expects to interact with the product. Consider:
- Entry point: How do they access it? (browser, CLI, IDE extension, mobile app)
- Session length: Quick lookup (seconds) vs deep work (hours)
- Integration: What other tools are they using simultaneously?
- Expertise assumption: Do they want guidance or get out of their way?
-->

<!-- AI: e.g., "Alex expects to access the tool directly from VS Code, without switching contexts. Sessions are typically 30 seconds to 5 minutes. They're comfortable with keyboard shortcuts and expect power-user features. They want minimal onboarding - they'll figure it out." -->

### Success Indicators

<!-- AI:
How will you know this persona is satisfied? Define observable signals.
-->

| Signal | Indicates |
|--------|-----------|
| <!-- AI: e.g., "Uses product daily" --> | <!-- AI: e.g., "It's valuable enough to integrate into workflow" --> |
| <!-- AI: e.g., "Recommends to colleagues" --> | <!-- AI: e.g., "Actively solves their problem" --> |
| <!-- AI: e.g., "Upgrades to paid tier" --> | <!-- AI: e.g., "Worth paying for" --> |

---

## Secondary Personas

<!-- AI:
Secondary personas are users you'll support but not optimize for in MVP. Their needs matter but shouldn't drive core decisions.

Include secondary personas if:
- They're a significant portion of expected users (> 20%)
- Supporting them doesn't conflict with primary persona
- They may become primary in future versions
-->

### Secondary Persona 1

| Attribute | Value |
|-----------|-------|
| **Name** | <!-- AI: e.g., "Jordan Smith" --> |
| **Role** | <!-- AI: e.g., "Junior developer, first job" --> |
| **Primary Need** | <!-- AI: e.g., "Learning while doing, needs more guidance" --> |
| **Difference from Primary** | <!-- AI: e.g., "Less technical, needs more explanation" --> |
| **Priority for MVP** | <!-- AI: Low/Medium --> |

### Secondary Persona 2 (if applicable)

<!-- AI: Add more secondary personas as needed. Delete this section if not applicable. -->

| Attribute | Value |
|-----------|-------|
| **Name** | <!-- AI: persona name --> |
| **Role** | <!-- AI: role --> |
| **Primary Need** | <!-- AI: need --> |
| **Difference from Primary** | <!-- AI: difference --> |
| **Priority for MVP** | <!-- AI: Low/Medium --> |

---

## Anti-Personas

<!-- AI:
Anti-personas define who this product is NOT for. This is just as important as defining target users. It prevents:
- Scope creep from edge-case requests
- Diluting the experience for primary users
- Wasted effort on unlikely conversions

Categories to consider:
- Wrong skill level (too technical or not technical enough)
- Wrong use case (enterprise when you're building for individuals)
- Wrong expectations (want features you explicitly won't build)
- Economic mismatch (can't/won't pay, or need enterprise features)
-->

### Who This Is NOT For

| Anti-Persona | Why They're Not a Fit | How to Recognize |
|--------------|----------------------|------------------|
| <!-- AI: e.g., "Enterprise procurement teams" --> | <!-- AI: e.g., "We don't have compliance certifications, SLAs, or SSO" --> | <!-- AI: e.g., "Ask about SOC2, vendor questionnaires" --> |
| <!-- AI: e.g., "Complete beginners" --> | <!-- AI: e.g., "We assume baseline technical knowledge" --> | <!-- AI: e.g., "Need explanation of basic concepts" --> |
| <!-- AI: e.g., "Users who need offline access" --> | <!-- AI: e.g., "Product requires internet connection" --> | <!-- AI: e.g., "Ask about airplane mode, restricted networks" --> |

### Handling Anti-Persona Inquiries

<!-- AI:
When anti-personas reach out, how should you respond? Be helpful without over-promising.
-->

| Situation | Response |
|-----------|----------|
| <!-- AI: e.g., "Enterprise asks about SSO" --> | <!-- AI: e.g., "Acknowledge the need, add to roadmap consideration, don't commit" --> |
| <!-- AI: e.g., "Beginner needs hand-holding" --> | <!-- AI: e.g., "Point to learning resources, suggest when they might be ready" --> |

---

## Persona Validation Plan

<!-- AI:
Personas should be validated, not assumed. Plan to verify your assumptions.
-->

| Assumption | Validation Method | Status |
|------------|-------------------|--------|
| <!-- AI: e.g., "Primary persona uses VS Code" --> | <!-- AI: e.g., "Survey during onboarding" --> | <!-- AI: Planned/In Progress/Validated --> |
| <!-- AI: e.g., "Pain point #1 is most important" --> | <!-- AI: e.g., "User interviews" --> | <!-- AI: Planned/In Progress/Validated --> |

---

## Related Documents

| Doc | Relationship |
|-----|--------------|
| [01-vision-and-goals.md](./01-vision-and-goals.md) | Problem statement defines who has the problem |
| [03-product-requirements.md](./03-product-requirements.md) | Requirements should address persona pain points |
| [04-feature-breakdown.md](./04-feature-breakdown.md) | Features should map to use cases |
| [05-ui-ux-design.md](./05-ui-ux-design.md) | UI should match persona expectations |
| [13-accessibility.md](./13-accessibility.md) | Accessibility needs may vary by persona |
| [AGENT-GUIDE.md](./AGENT-GUIDE.md) | How to lead the discovery process |

---

## AI Agent Instructions

### How to Complete This Document

1. **Start with real data if available** - Check if user has conducted interviews or has analytics. Use that first.

2. **One primary persona** - Resist the urge to define multiple "primary" users. Pick one.

3. **Be specific** - Vague personas like "developers" are useless. Get to job title, team size, technical level.

4. **Focus on behavior, not demographics** - Age and gender rarely matter for software. Focus on what they do, not who they are.

5. **Define anti-personas early** - This prevents scope creep. When someone suggests a feature, you can check if it serves the target persona.

### Questions to Ask the User

**For Primary Persona:**
- "Describe someone who would use this daily. What's their job title?"
- "What tools are they using today to solve this problem?"
- "What's the most frustrating part of their current workflow?"
- "How would they discover your product?"

**For Use Cases:**
- "Walk me through a typical day. When would they reach for this tool?"
- "What's the most common task? The most important?"
- "What would make them stop using the product?"

**For Anti-Personas:**
- "Who might want this but shouldn't use it? Why?"
- "What kind of feature requests should we push back on?"

### Document Completion Checklist

- [ ] Primary persona has specific name, role, and company context
- [ ] At least 3 pain points with measurable impact
- [ ] At least 3 use cases with frequency estimates
- [ ] Workflow expectations describe how they'll interact with the product
- [ ] At least 2 anti-personas defined with clear disqualifiers
- [ ] Validation plan exists for key assumptions
- [ ] No remaining [TBD] markers (or explicitly deferred with reason)
