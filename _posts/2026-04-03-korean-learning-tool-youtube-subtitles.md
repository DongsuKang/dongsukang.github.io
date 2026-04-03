---
title: "How I Built a Korean Learning Tool with YouTube Subtitles"
excerpt: "Building tubelang.com — a free tool to search Korean expressions and see them in real YouTube clips by native speakers"

categories:
  - Projects

toc: true
toc_sticky: true

use_math: false
comments: true
image: true
sitemap:
changefreq: daily
---

## The Problem with Textbook Korean

After studying Korean for years, I noticed a persistent gap: textbooks teach clean, scripted Korean, but native speakers sound completely different. The same expression — like 괜찮아요 — carries different emotional weight depending on tone, context, and relationship.

No textbook can capture that. But YouTube can.

## What I Built

[Tubelang](https://tubelang.com) is a free tool that lets you search any Korean expression and see it used in real YouTube clips by native speakers.

The idea is simple: instead of reading a definition of 눈치 (Korea's concept of social awareness), you can **hear** multiple native speakers use it in authentic contexts. Instead of memorizing that 그냥 means "just," you can see its 5+ emotional variants in action.

## How It Works

1. **Search** any Korean expression (e.g., 대박, 서운해요, 어떡해)
2. **See** real YouTube clips where native speakers use it
3. **Hear** the tone, speed, and emotional loading that textbooks miss
4. **Compare** the same expression across different speakers and contexts

## Expression Guides

I also created deep-dive guides for the most commonly misunderstood expressions:

- [괜찮아요](https://tubelang.com/korean-expressions/en/gwaenchanayo) — Almost never means "I'm fine"
- [그냥](https://tubelang.com/korean-expressions/en/geunyang) — The most untranslatable word in Korean
- [눈치](https://tubelang.com/korean-expressions/en/nunji) — Korea's social intelligence
- [대박](https://tubelang.com/korean-expressions/en/daebak) — 6 emotional tones, same word
- [서운해요](https://tubelang.com/korean-expressions/en/seounhaeyo) — The emotion English can't translate

Each guide includes real video clips, pronunciation, usage notes, and FAQ.

## Tech Stack

- **Frontend**: Next.js with TypeScript
- **Data Pipeline**: Python CLI for YouTube subtitle ingestion
- **Database**: Supabase (PostgreSQL)
- **Hosting**: Vercel

## Try It

[tubelang.com](https://tubelang.com) — Free, no signup required.

If you're learning Korean and tired of textbook examples that don't match real life, give it a try. Search any expression and hear how native speakers actually use it.
