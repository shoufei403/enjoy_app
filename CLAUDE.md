# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Environment Setup

**Required: Python 3.11.0**
```bash
pyenv install 3.11.0
pyenv local 3.11.0
python -m venv .venv3_11
source .venv3_11/bin/activate
```

**Electron Sandbox Configuration:**
```bash
export ELECTRON_DISABLE_SANDBOX=false
```

## Common Commands

### Development
- `yarn install` - Install dependencies
- `yarn start` - Start the application in development mode
- `yarn dev` - Start with local development server (WEB_API_URL=http://localhost:3000)

### Building and Packaging
- `yarn package` - Package the application
- `yarn make` - Create distributable packages
- `yarn publish` - Publish releases (requires GitHub/S3 credentials)

### Testing
- `yarn test` - Run all Playwright E2E tests
- `yarn test:main` - Run main process tests
- `yarn test:renderer` - Run renderer process tests

### Code Quality
- `yarn lint` - Run ESLint
- `yarn create-migration` - Create database migrations

### Asset Management
- `yarn download-dictionaries` - Download required dictionary files

## Architecture Overview

**Enjoy** is an AI-powered English learning desktop application built with Electron.

### Core Technologies
- **Frontend**: React 18 + TypeScript + Vite
- **Desktop**: Electron 34
- **Styling**: Tailwind CSS + Radix UI components
- **Database**: SQLite with Sequelize ORM
- **Testing**: Playwright for E2E testing
- **Audio**: FFmpeg, Wavesurfer.js, Azure Speech SDK

### Application Structure

#### Main Process (`src/main/`)
- `main.ts` - Application entry point, protocol handlers
- `window.ts` - Window management and browser window configuration
- `db/` - Database models and migrations using Sequelize
- `providers/` - Service providers for dictionaries, AI, etc.
- Key modules:
  - `settings.ts` - Application configuration
  - `echogarden.ts` - Speech processing and TTS
  - `ffmpeg.ts` - Audio/video processing
  - `downloader.ts` - Media downloading utilities

#### Renderer Process (`src/renderer/`)
- `app.tsx` - Main application component with context providers
- `components/` - UI components (26 component directories)
- `pages/` - Application pages and routing
- `context/` - React context providers (Theme, Settings, Database, etc.)
- `hooks/` - Custom React hooks
- `lib/` - Utility libraries and helpers

#### Key Features
1. **Audio Processing**: Recording, playback, waveform visualization, speech recognition
2. **AI Integration**: Multiple AI providers (OpenAI, Azure, local models)
3. **Document Learning**: EPUB, HTML, TXT processing with vocabulary extraction
4. **Video Learning**: YouTube integration with subtitle processing
5. **Dictionary Support**: Multiple dictionary formats (MDict, Cambridge, etc.)

### Database Architecture
- Uses SQLite with Sequelize ORM
- Models in `src/main/db/models/`
- Migrations managed with Umzug
- Supports multiple entity types: users, media items, learning progress, etc.

### Context Providers
The app uses multiple React context providers:
- `DbProvider` - Database access
- `ThemeProvider` - UI theming
- `AISettingsProvider` - AI configuration
- `DictProvider` - Dictionary management
- `CopilotProvider` - AI assistant functionality

### Asset Management
- Dictionary files stored in `lib/dictionaries/`
- Media files managed in user's library directory
- FFmpeg and other binaries bundled with the application

## Development Notes

### File Protocol
The app uses a custom `enjoy://` protocol for accessing local files and resources.

### Audio/Video Processing
Heavy reliance on FFmpeg for media processing. Binary files are unpacked from asar for proper functioning.

### Internationalization
The app supports multiple languages with i18next. Translations are managed through the i18n system.

### Error Tracking
Bugsnag is integrated for error reporting in production builds.

### Security
- Electron fuses configured for security
- Custom protocol with proper privileges
- Content Security Policy implemented