# Remote Agents with ChatGPT

So turns out ChatGPT already has built-in support for running Codex CLI agents remotely. The basic idea is that you can use your phone to orchestrate Codex CLI sessions running on a laptop or desktop. In my case my desktop is already being treated like a discount server, so the path would be `phone` -> `desktop`.

Here are the general steps for the setup:

- have the standard `ChatGPT` Android app installed on the phone
- have the `ChatGPT` desktop app installed on the Linux desktop
- have the Codex CLI app installed on the Linux desktop (this might be auto-installed by the desktop app? Not sure)
- link phone client to desktop client

## Installation

### Install `ChatGPT` on Android

- go to the Google Play Store
- hit the search button on the bottom nav bar
- search `chatgpt`
- hit install
- open the app
- login (mine uses Google for auth)

### Install `ChatGPT` Desktop

- go to the [ChatGPT downloads page](https://chatgpt.com/download/)
- select the package type for your desktop (mine is Fedora, so I choose `x64 (.rpm)`)
- open a terminal
- install from the package: `sudo dnf install ~/Downloads/chatgpt.x86_64.rpm`
- open that sucker up
- do whatever auth steps are needed (mine is Google, requires Google Auth number)

### Install Codex CLI (maybe optional?)

I installed Codex CLI first, so no idea if this step is required. It might get set up automatically by the desktop client? Anyways, here is the process to CYA.

- use the standalone installer: `curl -fsSL https://chatgpt.com/codex/install.sh | sh`
- as an alternative, using Homebrew: `brew install --cask codex`
- check if codex is installed: `codex --version`
- authenticate, preferably via the browser (use Google for this)

**NOTE**: highly unwise to use an `OPEN_API_KEY` for auth since OpenAI will bill you PER TOKEN instead of using your standard 5 hour/weekly window system for agents. Your wallet will thank you later.

### Link Phone to Desktop

Linking things in the modern era is so awesome. QR codes are absolutely GOATed.

- open `ChatGPT` on phone
- select `Remote` in the left sidebar
- select `I'm signed in on desktop`
- select `I have a pairing code`
- on desktop, open the `ChatGPT` client
- go to `File` -> `Settings` -> `Coding` -> `Connections`
- select `Add` in the `Allow connections` section
- scan the QR code with your phone
- on phone, select `Enable device unlock`
- do biometrics or whatever
- profit ???

This is so cool. Now do whatever you want with agents remotely!
