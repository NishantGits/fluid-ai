# Fluid AI

**The beautiful, privacy-first, open-source AI chat app — for everyone.**

<img src="/readme/screenshot.png" alt="Fluid AI Chat Interface" width="100%"/>
<img src="/readme/login.png" alt="Fluid AI Login Screen" width="100%"/>

Fluid AI is a modern, fast, and fully local-capable chat interface that works with **OpenAI, Gemini, Anthropic, Grok, Ollama and more** — all in one clean UI.

### Why Fluid AI?
- Private by default — your chats never leave your device unless you want them to  
- Works 100% offline with local models (Ollama)  
- Stores on Supabase (easy to migrate)
- Beautiful, responsive design with dark and light mode

### Updates
Check the Updates for the Fluid AI Instance (npm) in UPDATES.md. More updates are on the way!

## 🚀 Quick Start (Local Development)

### Prerequisites
- Node.js **v18 or v20** (avoid v19)
- Supabase
- Docker Desktop (for local Supabase)


## Local Quickstart

Follow these steps to get your own Fluid AI instance running locally.

### 1. Download

```bash
npm i -g @fluid-ai/chat
```

### 2. Install Dependencies

Open a terminal in the root directory of the Fluid AI instance and run:

```bash
npm install 
```
OR

```bash
npm i
```

### 3. Install Supabase & Run Locally

#### Why Supabase?

Usually, we would use local browser storage to store data. However, this is not a good solution for a few reasons:

- Security issues
- Limited storage
- Limits multi-modal use cases

We now use Supabase because it's easy to use, it's open-source, it's Postgres, and it has a free tier for hosted instances.

We will support other providers in the future to give you more options.

#### 1. Install Docker

You will need to install Docker to run Supabase locally. You can download it [here](https://docs.docker.com/get-docker) for free.

#### 2. Install Supabase CLI

**MacOS/Linux**

```bash
brew install supabase/tap/supabase
```

**Windows**

```bash
scoop bucket add supabase https://github.com/supabase/scoop-bucket.git
scoop install supabase
```

#### 3. Start Supabase

In your terminal at the root of your local Fluid AI instance, run:

```bash
supabase start
```

### 4. Fill in Secrets

#### 1. Environment Variables

In your terminal at the root of your local Fluid AI instance, run:

```bash
cp .env.local.example .env.local
```

Get the required values by running:

```bash
supabase status
```

Note: Use `API URL` from `supabase status` for `NEXT_PUBLIC_SUPABASE_URL`

Now go to your `.env.local` file and fill in the values.

If the environment variable is set, it will disable the input in the user settings.

#### 2. SQL Setup (NOT NECESSARY)
When you delete a file you uploaded (image, PDF, etc.), the file is removed from the chat UI but the actual file stays in Supabase Storage forever (it takes ~0.1 MB).
This step fixes this error, but it is not nessacary. 


In the 1st migration file `supabase/migrations/20240108234540_setup.sql` you will need to replace 2 values with the values you got above:

- `project_url` (line 53): `http://supabase_kong_chatbotui:8000` (default) can remain unchanged if you don't change your `project_id` in the `config.toml` file
- `service_role_key` (line 54): You got this value from running `supabase status`

This prevents issues with storage files not being deleted properly.

### 5. Install Ollama (optional for local models)

Download [here](https://ollama.com).

### 6. Run app locally

In your terminal at the root of your local Fluid AI instance, run:

```bash
npm run chat
```

Your local instance of Fluid AI should now be running at [http://localhost:3000](http://localhost:3000). Be sure to use a compatible node version (i.e. v18).

You can view your backend GUI at [http://localhost:54323/project/default/editor](http://localhost:54323/project/default/editor).

