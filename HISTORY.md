# Project History

This is the story of my journey using the latest AI coding agents to achieve a perfect 100% Lighthouse score with a real-life project: a mobile application (PWA) that lets small user groups share their secret places.

## Installation

Installing Github Spec Kit

## Constitution

This is the first step of the design process for this project using Github Spec Kit.

I spent quite a lot of time refining these guidelines, because the first results were quite over the top and not suited to my use case.

Overall, I would argue that the recommendation of a YouTube user is quite right for this phase: if you have a clear idea of your tech stack, run the installation script with a minimal template showcasing all of your technical choices. This way, the Github Agent will start on firm foundations and will not produce specifications for a totally different framework.

I have used Gemini 2.5 as the LLM model and overall was not totally satisfied with its output. It is a bit slow and tends to over-complicate things (or maybe the responsibility is really solely on Github Spec, I don't know).

In the end, here is the summary of my session:

```md
✦ I have created the AGENTS.md file at the root of the project, which summarizes all the
  coding guidelines we have defined.

> /quit

╭──────────────────────────────────────────────────────────────────────────────────────────────────╮
│                                                                                                  │
│  Agent powering down. Goodbye!                                                                   │
│                                                                                                  │
│  Interaction Summary                                                                             │
│  Session ID:                 xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx                                │
│  Tool Calls:                 62 ( ✓ 61 x 1 )                                                     │
│  Success Rate:               98.4%                                                               │
│  User Agreement:             100.0% (36 reviewed)                                                │
│  Code Changes:               +299 -2653                                                          │
│                                                                                                  │
│  Performance                                                                                     │
│  Wall Time:                  13h 29m 43s                                                         │
│  Agent Active:               16m 2s                                                              │
│    » API Time:               12m 15s (76.4%)                                                     │
│    » Tool Time:              3m 46s (23.6%)                                                      │
│                                                                                                  │
│                                                                                                  │
│  Model Usage                  Reqs   Input Tokens  Output Tokens                                 │
│  ───────────────────────────────────────────────────────────────                                 │
│  gemini-2.5-pro                 75      3,921,907         41,820                                 │
│  gemini-2.5-flash                2         10,886          3,711                                 │
│                                                                                                  │
│  Savings Highlight: 2,612,988 (66.4%) of input tokens were served from the cache, reducing       │
│  costs.                                                                                          │
│                                                                                                  │
│  » Tip: For a full token breakdown, run `/stats model`.                                          │
│                                                                                                  │
╰──────────────────────────────────────────────────────────────────────────────────────────────────╯
```