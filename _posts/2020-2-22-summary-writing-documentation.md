---
title: 'Summary: "What nobody tells you about documentation"'
category: "notes"
tags: ["writing", "documentation", "programming"]
desc: This article tries to summaries "What nobody tells you about documentation"
poster: documentation.jpg
issue_no: 2
---

The article ["What nobody tells you about documentation"](https://www.divio.com/blog/documentation) details on writing manuals for software. It provides details of different it's components, their intent, content, scope and purpose. This simplifies the process by helping writer have right mindset.

# Types of Documentation

## Tutorial

- Example: readme.
- Level: beginner.
- Orientation: to learn.
- Purpose: practical + to study.

### \* Dos:

- Doorway to your software for any user (setup/installation should be included).
- Multiple tasks (task: short set of steps).
- Should have simple tasks.
- Should reward user with knowledge.
- Should work 100% (makes user confident).

### \* Do nots:

- Need not use best practice if not required (complicates process).
- Do not explain beyond what is required (makes tutorial long).

## How to guides

- Example: how to print integer.
- Level: intermediate.
- Orientation: goal.
- Purpose: practical + for work.

### \* Dos:

- Should be working (can be part of test-cases).
- Should have proper heading (possible search phrase).
- Should setup/installation (intermediate level).
- Should be flexible (include small variation).

### \* Do nots:

- Should not explain more (link to api documentation).

## Explanation

- Example: api docs.
- Level: experienced.
- Orientation: technical details.
- Purpose: theory + to study.

### \* Dos:

- Should be code based (auto generate is better).
- Example if required (for edge case which is difficult to describe).
- Consistent structure (helps reading).

### \* Do nots:

- Should not explain about design decision (explain what code does, not why).
- Should not be goal oriented (put it in how to guide).

## Reference

- Example: white paper.
- Level: advanced expert.
- Orientation: to inform.
- Purpose: theory + working.

### \* Dos:

- Include discussions.
- Include design decision (including alternatives).
- Include historical reasons.
- Include good practices.
