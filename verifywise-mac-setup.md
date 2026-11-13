# How to install and set up VerifyWise on a Mac

This guide is written for someone who is new to GitHub, Terminal, and local development.

## Quick note: GitHub vs Git

- **GitHub** is the website where the code lives.
- **Git** is the tool your Mac uses to download and work with the code.

You do **not** install “GitHub” as an app for this project.
You may use the website to download the code, and you install Git only if you want the full developer workflow.

## What you need

- a Mac with a few gigabytes of free space
- internet access
- your Mac password for installing software
- patience for the first setup

If the Mac is a little older, that is usually okay. The first install may just take a bit longer.

## 1) Open Terminal

Terminal is where you type commands.

To open it:

1. Press **Command + Space**
2. Type **Terminal**
3. Press **Enter**

You can paste commands into Terminal with **Command + V**.

## 2) Install Homebrew

Homebrew is a package manager for Mac. It makes installing tools much easier.

If Homebrew is not already installed, paste this into Terminal:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

When it finishes, Terminal may tell you to add Homebrew to your path. Follow the on-screen instructions.

## 3) Install the main tools

Install the tools the repo uses most often:

```bash
brew install git node@22 python@3.12
brew install --cask docker
```

Then open **Docker Desktop** once from Applications and let it finish starting.

## 4) Check that the tools work

Run these commands one by one:

```bash
git --version
node -v
npm -v
python3 --version
docker --version
```

If one of them says “command not found,” that tool is not installed correctly yet.

## 5) Get the repo onto your Mac

You have two choices.

### Option A: easiest

1. Open the repo page in your browser.
2. Click **Code**.
3. Click **Download ZIP**.
4. Unzip the file.
5. Move the folder somewhere easy to find, like Documents.

### Option B: better for learning Git

If Git is installed, use Terminal and run:

```bash
git clone https://github.com/verifywise-ai/verifywise.git
```

Then open the downloaded folder.

## 6) Open the repo in Terminal

If you downloaded the ZIP, use `cd` to move into the folder.

Example:

```bash
cd ~/Documents/verifywise
```

If you used `git clone`, enter the cloned folder instead.

## 7) Install dependencies

VerifyWise has separate parts.

### Frontend

```bash
cd Clients
npm install
```

### Backend

Open a second Terminal window or tab, then run:

```bash
cd Servers
npm install
```

### EvalServer

Open a third Terminal window or tab:

```bash
cd EvalServer
cp .env.example .env
python3.12 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### AIGateway

Open a fourth Terminal window or tab:

```bash
cd AIGateway
cp .env.example .env
python3.12 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

## 8) Create the environment files

The repo includes `.env.example` files to show what settings are needed.

A simple rule:

- copy the example file
- name the copy `.env`
- fill in real values

The most important file for local development is usually `Servers/.env`.

If you are just learning, start with the defaults from the example files and change only what you need.

## 9) Start the supporting services

VerifyWise uses PostgreSQL and Redis.

The easiest way on a Mac is to use Docker Desktop.

You can start containers from Terminal, or use Docker Desktop’s app interface.

If you want to use Terminal, follow the repo’s README and create:

- a PostgreSQL container
- a Redis container

The README also explains which ports the app uses:

- frontend: `5173`
- backend: `3000`
- database: `5432`
- Redis: `6379`
- EvalServer: `8000`
- AI Gateway: `8100`

## 10) Start the app

A simple local order is:

1. start Docker Desktop
2. start PostgreSQL and Redis
3. start the backend
4. start the frontend
5. start EvalServer and AIGateway if you want the full stack

Typical commands are:

### Backend

```bash
cd Servers
npm run watch
```

### Frontend

```bash
cd Clients
npm run dev
```

### EvalServer

```bash
cd EvalServer/src
source ../venv/bin/activate
alembic upgrade head
uvicorn app:app --host 0.0.0.0 --port 8000 --reload
```

### AIGateway

```bash
cd AIGateway/src
source ../venv/bin/activate
alembic upgrade head
uvicorn app:app --host 0.0.0.0 --port 8100 --reload
```

If the app is running correctly, the browser should be able to open the frontend on `http://localhost:5173`.

## 11) If you only want the learning project

If the full stack feels like too much on day one, you can still do the project with just:

- the repo files
- the README
- the overview document
- the project document

That is enough to learn the ideas before you run everything locally.

## 12) Safety and virus-check tips

If you want to be careful, use this checklist:

- only download from the official GitHub repo
- only use the repo’s own README and example env files
- do not run random scripts from the internet
- check that downloaded files came from `verifywise-ai/verifywise`
- keep macOS up to date
- let Docker, Homebrew, and the browser come from official sources only

Mac also has built-in security checks such as Gatekeeper and XProtect.
If a file or app looks suspicious, do not open it.

If you want an extra scan, you can use a trusted scanner like Malwarebytes, but that is optional.

## 13) Troubleshooting

### “command not found”

That usually means the tool is not installed yet or is not on your path.

### Docker is slow

That is common on older Macs. Close extra apps and give it a few minutes.

### A port is already in use

Another app may already be running on that port. Quit the old process or restart the computer.

### `npm install` fails

Check that you installed the right Node version.
The repo expects a modern Node 22+ release.

### `python3.12` is missing

Install Python 3.12 again or check whether Homebrew put it on your path.

## 14) The main idea to remember

You are not trying to memorize every command.
You are learning the basic loop:

1. install tools
2. download the repo
3. install dependencies
4. set env files
5. start the app
6. change something small
7. see what happens
