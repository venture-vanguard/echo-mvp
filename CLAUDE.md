# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Echo-MVP is a psychosocial risk monitoring system designed for workplace wellbeing, specifically targeting the funeral industry. The system provides 90-second phone/WhatsApp check-ins with workers to identify and address psychosocial hazards per ISO 45003 standards.

## Current State

This is an early-stage MVP repository that currently contains only planning documentation. The actual codebase implementation has not yet been started.

## Architecture & Planning

### Core Concept
- **Target**: ~30 funeral industry workers out of ~200 total staff for pilot
- **Method**: Weekly 90-second phone/WhatsApp check-ins
- **Privacy**: Crew-level analytics to supervisors, individual guidance stays private
- **Compliance**: ISO 45003 aligned for psychosocial hazard identification and control

### Pilot Structure
- **Treatment group** (n≈18): Full Echo experience
- **Control group** (n≈9): Business-as-usual measurement
- **Red-team group** (n≈6): Stress-testing with intentional gaming of prompts

### Key Features to Implement
- Outbound phone + WhatsApp channels (no worker app required)
- Agent-based conversational interface with human, respectful tone
- Crew-level heatmaps for supervisors
- ISO 45003 evidence pack generation for executives/board
- Named-by-exception escalation for imminent harm/safety risks
- Privacy-by-design with transparent data handling

## Development Approach

When implementing this system, consider:

1. **Privacy-first design**: All individual data remains private to worker, only cohort trends visible to management
2. **Minimal data collection**: Worker ID, name, mobile, team, site, manager, roster windows
3. **Security requirements**: Encryption in transit/at rest, auditable access logs
4. **Engagement optimization**: Pre-shift/break timing, 90-second limit, trust-building through action receipts

## Key Stakeholders & Considerations

- Founder sponsor, Operations lead, People & Culture, WHS, Communications
- Union/worker representative involvement
- EAP (Employee Assistance Program) integration
- Clear consent and opt-out mechanisms

## Success Metrics to Track

- Weekly active participation ≥60%
- Signal quality and false-positive containment
- Time-to-intervention for identified risks
- ISO 45003 psychosocial risk movement indicators
- Auditor-friendly evidence pack generation