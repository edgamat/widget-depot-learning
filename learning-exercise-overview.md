**Claude Code Integration**

A Structured Learning Exercise

# Overview

I want to evaluate Claude Code as a potential productivity tool for software development. Rather than adopting prescriptive guidance from external sources, I want to develop my own informed understanding of how Claude Code fits my workflow, codebase, and potentially teams I work with.

This document describes a structured learning exercise that will produce two deliverables: a good practices guide, and an assessment of where Claude Code adds the most value for me.

# Motivation

There is no shortage of advice about how to get the most out of AI coding tools. Articles, tutorials, and videos offer fully formed approaches, each presented as the best way to work. While this content is well-intentioned, I feel there is a risk in adopting someone else's workflow wholesale:

- I don't understand why each practice matters, only that I was told it does.
- I can't distinguish genuinely helpful techniques from those that simply sound compelling.
- I have no baseline to measure improvement against.

A hands-on approach lets me discover friction points, develop solutions grounded in actual experience, and build confidence in the practices I ultimately adopt.

I am approaching this as a collaborative exploration rather than a formal study. My goal is not to judge Claude Code but to develop fluency with it. I want to understand its strengths, its limitations, and how to set it up in a way that reflects how I work.

# Exercise Structure

The exercise is divided into phases, run sequentially, using a fake software project as the working codebase. The software project is described in a separate document. It is a rewrite of an existing (fake) website in a greenfield environment.

## Initial Phase

I will begin with a minimal setup: an empty repository, Claude Code installed, and no preconfigured context files, custom commands, or structured workflows. This mirrors the experience of a developer who has just discovered the tool.

The goal of this phase is to observe how to interact with Claude Code. I will maintain a **friction log** throughout, noting each time Claude Code required repeated re-orientation, produced unexpected results, or where missing context would have helped. These observations will become the raw material for each following Phase.

**What I plan to capture in each Phase**

- Where Claude needed context and I had to re-supply repeatedly
- Where outputs diverged from any conventions or architecture
- Where the absence of custom commands created unnecessary friction
- Where Claude Code genuinely accelerated my work without any special setup
- Approximate time spent per story: coding vs. prompting vs. correcting
- Usage statistics (tokens used?) per session

## Following Phases

At the end of each phase, I will pause development, review the friction log, and build out the scaffolding the previous experience tells me what I actually need. This may include updates to the CLAUDE.md file  ith project context and conventions, custom slash commands for recurring  workflows, and structured templates for common tasks such as story creation or test generation. I expect that I will end up using some of the 'advice' available to me from articles, tutorials and videos. I will try and focus on assessing their impact objectively.

I will then continue the same project with this improved setup into the next phase. I will attempt to evaluate improvements in productivity and output quality.

Due to the part-time nature of this learning exercise, a phase may last a few hours, a few days, or longer.

## Wrap-up Phase

In the final phase I will compare the observations, document what changed from beginning to end and why, and produce a good practices guide and readiness assessment.

# Deliverables

| **Good Practices Guide** | **Readiness Assessment** |
|---|---|
| A living document describing how Claude Code works best in my environment, grounded in my own observed experience. | An account of where Claude Code adds meaningful value for me, where it requires investment to use well, and what I would want other developers to know before adopting it. |

# How I Will Measure Progress

I am not running a controlled experiment (as much as I'd like to....). The team size (a single developer) and time constraints make that impractical. Instead, I am iterating at specific intervals based on observations throughout the project. Hopefully this will give a meaningful basis for comparison.

| **Objective Measures** | **Subjective Measures** |
|---|---|
| - Stories completed per phase | - Developer experience and confidence |
| - Time per story: coding vs. prompting | - Perceived output quality |
| - Defect rate and rework frequency | - Cognitive load during Claude sessions |
| - Number of Claude interactions per story | - Willingness to recommend the workflow |

# Constraints and Expectations

As a single developer contributing 4-8 hours per week, my total working capacity is limited. I expect to reach a meaningful first milestone on the software project, but the primary value of this exercise is the
documented learning, not the volume of code produced.

I am aware that Claude Code's Pro plan usage limits are sometimes a limiting factor. I will monitor usage and document any cases where limits affected my workflow, as this is itself a relevant finding.

# Timeline

| **Period** | **Phase** | **Focus** |
|---|---|---|
| Phase 1 | Naive Approach | Build with minimal setup; maintain friction log throughout |
| Phase 2, 3, ... N | Periodic Review | Evaluate observations; update CLAUDE.md and custom commands. Continue the project with improved setup; track changes in experience |
| Final Phase | Report my findings | Compare phases; produce good practices guide and readiness assessment |
