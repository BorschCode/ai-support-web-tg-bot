# 🤖 AI Support Bot

> A powerful multi-channel AI support bot powered by Google Gemini AI. Provide instant, intelligent support to your users via web chat or Telegram - all from a single, unified platform.

[![Laravel](https://img.shields.io/badge/Laravel-12-FF2D20?style=flat&logo=laravel)](https://laravel.com)
[![Vue.js](https://img.shields.io/badge/Vue.js-3-4FC08D?style=flat&logo=vue.js)](https://vuejs.org)
[![Gemini AI](https://img.shields.io/badge/Gemini-AI-4285F4?style=flat&logo=google)](https://ai.google.dev)
[![Telegram](https://img.shields.io/badge/Telegram-Bot-26A5E4?style=flat&logo=telegram)](https://telegram.org)

## 📋 Table of Contents

- [Features](#-features)
- [Screenshots](#-screenshots)
- [Tech Stack](#-tech-stack)
- [Quick Start](#-quick-start)
- [Installation](#-installation)
- [Telegram Bot Setup](#telegram-bot-setup)
- [Usage](#usage)
- [Development](#development)
- [Testing](#running-tests)
- [API Documentation](#api-endpoints)
- [Configuration](#configuration)
- [Troubleshooting](#troubleshooting)

## ✨ Features

- 🤖 **AI-Powered Responses** - Leverages Google Gemini 2.0 Flash for intelligent, context-aware conversations
- 💬 **Multi-Channel Support** - Seamlessly handle support requests from both web browser and Telegram
- 📝 **Conversation History** - All conversations are persisted and easily retrievable for context continuity
- 📊 **Usage Analytics** - Built-in message statistics tracking for billing and monitoring purposes
- 🌙 **Dark Mode** - Complete dark mode support with automatic theme switching
- 🔒 **Session Management** - Secure, session-based conversation tracking across channels
- ⚡ **Real-time Updates** - Instant message delivery and response with WebSocket support
- 🎨 **Modern UI/UX** - Beautiful, responsive interface built with Tailwind CSS 4

## 📸 Screenshots

### Landing Page
Modern, professional landing page with clear call-to-actions and feature showcase.

![AI Support Bot - Landing Page](./readme/index.png)

**Features visible:**
- Clean, gradient-based design with dark mode support
- Feature highlights with icons
- Live chat preview
- Dual CTAs for web and Telegram access
- Statistics display

---

### Interactive Chat Interface
Real-time chat interface with conversation history and AI-powered responses.

![AI Support Bot - Chat Interface](./readme/chat.png)

**Features visible:**
- Clean message bubbles (user vs AI)
- Conversation history
- Session-based chat tracking
- Responsive textarea with keyboard shortcuts
- Loading states during AI processing
- Sidebar navigation with Home, Chat, and Dashboard links

## 🛠️ Tech Stack

| Category | Technology |
|----------|-----------|
| **Backend Framework** | Laravel 12 |
| **PHP Version** | 8.4 |
| **Frontend Framework** | Vue.js 3 |
| **UI Library** | Inertia.js v2 |
| **Styling** | Tailwind CSS 4 |
| **AI Engine** | Google Gemini 2.0 Flash Experimental |
| **Telegram Integration** | Telegraph (defstudio/telegraph) |
| **Database** | MySQL 8.0 |
| **Testing Framework** | Pest v4 |
| **Development Environment** | Laravel Sail (Docker) |
| **Type Safety** | PHPStan (Static Analysis) |

## 🚀 Quick Start

```bash
# Clone and setup
git clone <your-repo-url>
cd tg-ai-support-bot
composer install
cp .env.example .env

# Configure your API keys in .env
# - GEMINI_API_KEY
# - TELEGRAM_TOKEN
# - VITE_TELEGRAM_BOT_USERNAME

# Start development environment
vendor/bin/sail up -d
vendor/bin/sail artisan key:generate
vendor/bin/sail artisan migrate
npm install && npm run dev

# Visit http://localhost:8060
```

## 📦 Installation

### Prerequisites

Before you begin, ensure you have the following installed:

| Requirement | Version | Purpose |
|------------|---------|---------|
| Docker & Docker Compose | Latest | Laravel Sail environment |
| Composer | 2.x | PHP dependency management |
| Node.js | 18.x or higher | Frontend build tools |
| npm | 9.x or higher | Package management |

**Required API Keys:**
- 🔑 **Google Gemini API Key** - Get it from [Google AI Studio](https://makersuite.google.com/app/apikey)
- 🤖 **Telegram Bot Token** - Create a bot with [@BotFather](https://t.me/BotFather)

### Setup Steps

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd tg-ai-support-bot
   ```

2. **Install PHP dependencies**
   ```bash
   composer install
   ```

3. **Copy environment file**
   ```bash
   cp .env.example .env
   ```

4. **Configure environment variables**

   Edit `.env` and configure the following required variables:

   | Variable | Description | Example | Required |
   |----------|-------------|---------|----------|
   | `GEMINI_API_KEY` | Your Google Gemini API key | `AIzaSyA...` | ✅ Yes |
   | `TELEGRAM_TOKEN` | Telegram bot token from @BotFather | `123456:ABC-DEF...` | ✅ Yes |
   | `VITE_TELEGRAM_BOT_USERNAME` | Your bot's username (without @) | `my_support_bot` | ✅ Yes |
   | `APP_URL` | Your application URL | `http://localhost:8060` | ⚠️ For webhooks |
   | `MYSQL_EXTRA_OPTIONS` | MySQL configuration options | `""` | ✅ Yes |

   **Get your API credentials:**
   - 🔑 Gemini API: https://makersuite.google.com/app/apikey
   - 🤖 Telegram Bot: https://t.me/BotFather

   **Example `.env` configuration:**
   ```env
   GEMINI_API_KEY="AIzaSyDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
   TELEGRAM_TOKEN="7123456789:AAExxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
   VITE_TELEGRAM_BOT_USERNAME="my_support_bot"
   MYSQL_EXTRA_OPTIONS=""
   ```

   > **💡 Tip:** The bot username can include or exclude the @ symbol - it will be stripped automatically

5. **Start Laravel Sail**
   ```bash
   vendor/bin/sail up -d
   ```

6. **Generate application key**
   ```bash
   vendor/bin/sail artisan key:generate
   ```

7. **Run migrations**
   ```bash
   vendor/bin/sail artisan migrate
   ```

8. **Install Node dependencies**
   ```bash
   npm install
   ```

9. **Build frontend assets**
   ```bash
   npm run build
   # or for development
   npm run dev
   ```

## 📱 Telegram Bot Setup

### Step 1: Create Your Bot

1. Open Telegram and find [@BotFather](https://t.me/BotFather)
2. Send the `/newbot` command
3. Follow the prompts to set your bot name and username
4. Copy the **API token** you receive (format: `123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11`)
5. Add the token to your `.env` file as `TELEGRAM_TOKEN`

### Step 2: Register Bot in Database

```bash
vendor/bin/sail artisan tinker
```

Then execute:
```php
// Create the bot record
$bot = \DefStudio\Telegraph\Models\TelegraphBot::create([
    'token' => config('services.telegram.token'),
    'name' => 'AI Support Bot'
]);

// Register the webhook with Telegram
$bot->registerWebhook()->send();

// Verify registration (optional)
$bot->info()->send();
```

### Step 3: Configure Bot Commands (Optional)

Set up commands in @BotFather for better UX:

1. Send `/setcommands` to @BotFather
2. Select your bot
3. Send:
   ```
   start - Start conversation with the bot
   help - Get help and information
   ```

### Step 4: Customize Bot (Optional)

Enhance your bot's appearance:

```bash
# Set bot description
/setdescription to @BotFather

# Set bot profile picture
/setuserpic to @BotFather

# Set about text
/setabouttext to @BotFather
```

### Webhook URL

Your webhook URL will be automatically registered in the format:
```
https://your-domain.com/telegraph/{token}/webhook
```

For local development, you can use:
- ngrok: `ngrok http 8060`
- LocalTunnel: `lt --port 8060`

Update the webhook with your public URL:
```php
$bot->registerWebhook()->send();
```

## Usage

### Web Chat

1. Navigate to `http://localhost:8060` (or your configured APP_URL)
2. Click "Start Web Chat" button
3. Start chatting with the AI support bot

### Telegram Chat

1. Search for your bot in Telegram using the username you created
2. Send `/start` to begin
3. Start chatting with the bot

## Running Tests

```bash
# Run all tests
vendor/bin/sail artisan test

# Run specific test file
vendor/bin/sail artisan test tests/Feature/ChatTest.php

# Run with coverage
vendor/bin/sail artisan test --coverage
```

## Development

### Start Development Server

```bash
# Start all services (Laravel, Queue, Logs, Vite)
composer run dev
```

This will start:
- PHP development server (port 8000)
- Queue worker
- Log viewer (Pail)
- Vite dev server (HMR)

### Code Formatting

```bash
# Format code with Laravel Pint
vendor/bin/sail bash -c "vendor/bin/pint"
```

## API Endpoints

### Web Chat API

- `GET /chat` - Chat interface page
- `POST /api/chat/send` - Send message and get AI response
- `GET /api/chat/history/{sessionId}` - Get conversation history

### Telegram Webhook

- `POST /telegraph/{token}/webhook` - Telegram webhook (automatically configured)

## Database Schema

### Tables

- **conversations** - Stores conversation metadata
  - `id`, `channel` (web/telegram), `user_identifier`, `telegram_user_id`, `telegram_username`, `last_message_at`

- **messages** - Stores all messages
  - `id`, `conversation_id`, `role` (user/assistant), `content`, `created_at`

- **message_stats** - Billing statistics
  - `id`, `stat_date`, `channel`, `message_count`, `conversation_count`

## Architecture

### Service Layer

- **GeminiService** - Handles communication with Google Gemini API
- **ConversationService** - Manages conversations, messages, and statistics

### Controllers

- **ChatController** - Handles web chat requests
- **SupportBotHandler** - Handles Telegram webhook events (extends Telegraph's WebhookHandler)

### Frontend

- **Chat/Index.vue** - Main chat interface with message history and real-time updates
- **Welcome.vue** - Landing page with feature descriptions and CTAs

## Configuration

### Gemini API Settings

The Gemini service configuration is in `app/Services/GeminiService.php`:
```php
protected string $model = 'gemini-2.0-flash-exp'; // Current Gemini model

'temperature' => 0.7,
'topK' => 40,
'topP' => 0.95,
'maxOutputTokens' => 1024,
```

**Note:** The model uses the latest Gemini 2.0 Flash Experimental API. Make sure your API key has access to this model.

### Telegraph Settings

Configuration is in `config/telegraph.php`:
- Webhook handler: `App\Telegram\SupportBotHandler::class`
- Allow unknown chats: `true`
- Store unknown chats: `true`

## Troubleshooting

### Frontend Assets Not Found

If you see "Unable to locate file in Vite manifest":
```bash
npm run build
```

### Telegram Webhook Not Working

1. Check your bot token is correct in `.env`
2. Verify webhook is registered: `$bot->info()->send()`
3. Check webhook URL is publicly accessible
4. Review Laravel logs: `vendor/bin/sail artisan pail`

### Database Connection Issues

If using Docker/Sail, ensure containers are running:
```bash
vendor/bin/sail up -d
```

## License

This project is open-sourced software licensed under the MIT license.

## Support

For issues and questions, please open an issue on GitHub.
