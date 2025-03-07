## Publish to Itch.io ️🕹️ with Butler 🎩

<img alt="Itch.io" src="https://img.shields.io/badge/Itch.io-FA5C5C?style=for-the-badge&amp;logo=itch.io&amp;logoColor=white"><img alt="GitHub Actions" src="https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&amp;logo=github&amp;logoColor=white">

**The simplest way to publish your games to Itch.io directly from GitHub!**

This GitHub Action automates the entire process of deploying your game to [Itch.io](https://itch.io) by setting up [Butler](https://itch.io/docs/butler/) (*the official Itch.io command-line tool*) and handling the upload process - all with minimal configuration.

## ✨ Features
- 🤖 **Automatic Butler Setup** - No need to install or configure anything manually
- ️🖥️ **Cross-Platform Support** - Works on Windows, macOS, and Linux runners
- ️🏷️ **Version Tagging** - Optionally tag your releases with version numbers
- 🔒 **Secure** - Uses GitHub Secrets for API key protection

## 🔧 Usage

Add this to your workflow file:

```yaml
- uses: Oval-Tutu/publish-to-itch-with-butler@v1
  with:
    api-key: ${{ secrets.BUTLER_API_KEY }}
    itch_user: your-itch-username
    itch_game: your-game-name
    channel: windows
    package: ./build/windows/
    version: 1.0.0
```

## 📋 Parameters

| Parameter | Description | Required | Default |
| --------- | ----------- | -------- | ------- |
| `api-key` | Butler API key from Itch.io | ✅ | - |
| `channel` | Channel name (e.g., android, html, linux, osx, windows) | ✅ | - |
| `itch_user` | Your Itch.io username | ✅ | - |
| `itch_game` | Your game's name on Itch.io | ✅ | - |
| `package`   | Directory or file to upload | ✅ | - |
| `version`   | Game version (will be shown on Itch.io) | ❌ | "" |

## 🔐 Getting Your Butler API Key

1. Log in to [itch.io](https://itch.io)
2. Navigate to [your API keys](https://itch.io/user/settings/api-keys)
3. Generate a new API key
4. Add it to your repository secrets as `BUTLER_API_KEY`

## 📚 Example Workflow

```yaml
name: Deploy Game

on:
  release:
    types: [published]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      # Build your game...

      - uses: Oval-Tutu/publish-to-itch-with-butler@v1
        with:
          api-key: ${{ secrets.BUTLER_API_KEY }}
          itch_user: awesome-dev
          itch_game: awesome-game
          channel: windows
          package: ./build/
          version: ${{ github.event.release.tag_name }}
```

## 🌟 Supported Platforms

Only the x64 64-bit architecture is supported for Windows and Linux because Butler does provide builds for other architectures.

- 🐧 Linux
- 🍏 macOS
- 🪟 Windows

Get your games to your players faster than ever with automated Itch.io publishing!
