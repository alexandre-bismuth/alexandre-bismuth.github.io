---
title: "PickYourCourses — a Telegram Bot for Course Reviews"
date: 2025-07-01
tags: []
author: "Alexandre Bismuth"
description: "A Telegram bot for École Polytechnique students to share and read course reviews, running serverless on AWS Lambda."
summary: "A Telegram bot for École Polytechnique students to share and read course reviews — built in TypeScript and running serverless on AWS Lambda, DynamoDB, and API Gateway."
---

---

<div class="buttons" style="display:flex;flex-wrap:wrap;justify-content:space-between;gap:10px;margin:14px 0 10px 0;">
  <a class="button" style="flex:1;text-align:center;margin:0;padding:5px 10px;background:rgba(0,0,0,0.1);" href="https://github.com/alexandre-bismuth/PickYourCourses"><span class="button-inner">Code</span></a>
</div>

---

##### Overview

PickYourCourses is a Telegram bot for École Polytechnique students to share and read course reviews. It lets students browse courses, rate them, and vote on each other's reviews — all from within Telegram. The bot is written in TypeScript, organised into webhook handlers, data models, business-logic services, and utilities.

The project is fully open-source and built to be adaptable: anyone who would like to deploy the same course-review system for their own university is free to take the code, swap in their own course catalogue, and stand it up on their own infrastructure.

---

##### Features

- Course review system with ratings (overall, quality, difficulty)
- Course categorization and browsing
- Voting system for reviews
- Administrative functions
- Rate limiting and session management

---

##### Architecture

The bot is designed to run serverless on AWS Lambda, with:

- **DynamoDB** for data persistence
- **API Gateway** for webhook handling
- **CloudWatch** for logging and monitoring

The codebase is built and deployed through npm scripts (`build`, `dev`, `lint`, `deploy:dev`, `deploy:prod`), compiling TypeScript down to the `dist/` directory for deployment.
