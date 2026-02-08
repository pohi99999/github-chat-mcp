# GitHub Chat MCP – beállítás Cursor / GitHub Copilot Chat számára

## 1. Előfeltételek

- **uv** telepítve (Mac/Linux: `curl -LsSf https://astral.sh/uv/install.sh | sh`, Windows: PowerShell parancs a README-ből).
- Opcionális: GitHub Chat API kulcs (freemium esetén nem kötelező).

## 2. Cursor MCP konfiguráció

### A) Cursor GUI

1. **Cursor** → **Settings** (Ctrl+,) → **Features** → **MCP**.
2. **+ Add New MCP Server**.
3. Add meg:
   - **Name:** `github-chat`
   - **Command:** `uvx`
   - **Args:** `github-chat-mcp`

### B) Fájl szerkesztése

Másold a projekt gyökerében lévő **mcp.json** tartalmát a Cursor konfig fájlba:

**Windows:**
```
%USERPROFILE%\.cursor\config\mcp.json
```
Pl.: `C:\Users\<FELHASZNÁLÓNÉV>\.cursor\config\mcp.json`

**macOS/Linux:**
```
~/.cursor/config/mcp.json
```

Példa tartalom (ugyanaz, mint a projektben lévő **mcp.json**):

```json
{
  "mcpServers": {
    "github-chat": {
      "command": "uvx",
      "args": ["github-chat-mcp"]
    }
  }
}
```

Ha API kulcsot is használsz:

```json
{
  "mcpServers": {
    "github-chat": {
      "command": "uvx",
      "args": ["github-chat-mcp"],
      "env": {
        "GITHUB_API_KEY": "ghp_xxxxxxxxxxxxxxxxxxxx"
      }
    }
  }
}
```

## 3. Lokális fejlesztés (a repo klónjából)

Ha a szervert a projekt mappájából futtatod (pl. `G:\Brunella\github-chat-mcp`), a Cursor **mcp.json**-ben:

```json
{
  "mcpServers": {
    "github-chat": {
      "command": "uv",
      "args": [
        "--directory",
        "G:/Brunella/github-chat-mcp",
        "run",
        "github-chat-mcp"
      ],
      "env": {}
    }
  }
}
```

Windows-on a mappa útvonalat használhatod `/`-kel is (ahogy fent van).

## 4. Indítás után

1. Mentsd a konfigot, indítsd újra a Cursort.
2. A chaten így használhatod:
   - „Index the GitHub repository at https://github.com/username/repo”
   - „What is the core tech stack used in this repository?”

A projekt gyökerében lévő **mcp.json** ezt a konfigurációt tartalmazza; ezt másold a Cursor **mcp.json**-be a fenti helyre.
