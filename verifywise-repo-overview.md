# VerifyWise repo overview for a beginner

VerifyWise is **not** an AI model. It is a web app that helps people **govern AI**: keep track of AI systems, policies, risks, evidence, and compliance frameworks.

If your friend is interested in AI policy, this repo is useful because it shows how policy ideas turn into software.

## The short version

Think of VerifyWise as a place where an organization can answer questions like:

- What AI tools do we use?
- Who approved them?
- What risks do they create?
- What evidence do we have?
- Which rules or frameworks do we need to follow?

## What the main parts do

- **Clients/** — the browser UI. This is what a person clicks.
- **Servers/** — the backend API, database logic, authentication, and background jobs.
- **EvalServer/** — a Python service for LLM evaluations.
- **AIGateway/** — a Python service that routes model calls through guardrails and logging.
- **docs/** — architecture notes, guides, and user docs.

## How the app works in plain English

1. You click something in the browser.
2. The frontend sends a request to the backend.
3. The backend checks permissions and reads/writes the database.
4. Some features also call the evaluation service or AI gateway.
5. The UI updates based on the response.

That flow is useful to remember because it is the basic shape of many web apps.

## The main policy ideas hidden inside the app

These are the ideas your friend will keep seeing:

- **Use case** — where AI is being used.
- **Policy** — the rules for how AI should or should not be used.
- **Risk** — what could go wrong.
- **Control** — what you do to reduce the risk.
- **Evidence** — proof that you reviewed something or made a decision.
- **Framework** — a rule set such as EU AI Act, ISO 42001, NIST AI RMF, and others.

## Why this repo is good for learning coding

This repo is a good teaching example because it has:

- a real frontend and backend
- multiple files that work together
- data stored in a database
- a clear split between UI, logic, and services
- lots of places where a small change has a visible effect

That means your friend can learn both **policy thinking** and **how code is organized**.

## Good first files to read

If she wants to understand the repo without getting lost, start here:

1. `README.md`
2. `CLAUDE.md`
3. `Clients/CLAUDE.md`
4. `Servers/CLAUDE.md`
5. `docs/technical/domains/policies.md`
6. `docs/technical/domains/risk-management.md`
7. `docs/technical/domains/use-cases.md`

## What she should pay attention to first

When she opens code for the first time, she should look for:

- where a page lives in the frontend
- where the matching API route lives in the backend
- what data the page reads or writes
- what names are used for policy, risk, evidence, and framework features

## A beginner-friendly mental model

A good way to think about the repo is:

- **frontend** = the questions people ask the app
- **backend** = the rules the app follows
- **database** = the memory of the app
- **docs** = the explanation of the app

## What not to worry about on day 1

She does **not** need to understand everything at once.

It is okay to ignore these at first:

- Kubernetes
- deployment automation
- every compliance framework
- every integration
- every background job
- every advanced security setting

## A simple goal for learning

A very good first exercise is:

1. find one screen in the app,
2. find the code that renders it,
3. find the backend request it makes,
4. change one small thing,
5. reload the app and see the change.

That is how coding starts to feel real.

## If she only remembers three things

1. VerifyWise is a governance tool, not an AI model.
2. The repo is split into frontend, backend, and Python services.
3. Policy concepts like risk, controls, and evidence are all represented in code.
