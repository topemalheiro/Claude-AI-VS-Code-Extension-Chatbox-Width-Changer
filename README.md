# Claude Code VS Code Extension Mods

PowerShell scripts to customize the Claude Code VS Code extension UI.

## What This Does

By default, the Claude Code extension limits message width to 680px, creating a narrow centered column. These scripts modify the CSS to allow messages and the chat input to span the full width of the panel.

**Before:** Narrow 680px centered column
**After:** Full-width messages that use all available space

## Scripts

| Script | Target |
|--------|--------|
| `fix-message-width.ps1` | VS Code (stable) |
| `fix-message-width-insiders.ps1` | VS Code Insiders |

## Usage

Run the appropriate script for your VS Code version:

```powershell
# For VS Code (stable)
powershell -ExecutionPolicy Bypass -File "fix-message-width.ps1"

# For VS Code Insiders
powershell -ExecutionPolicy Bypass -File "fix-message-width-insiders.ps1"
```

Then reload VS Code:
1. Press `Ctrl+Shift+P`
2. Type "Developer: Reload Window"
3. Press Enter

## Re-running After Updates

The Claude Code extension updates frequently. Each update overwrites the CSS, so you'll need to re-run the script after updates to restore full-width messages.

## How It Works

The scripts modify the extension's `webview/index.css` file, changing the message container's `max-width` from `680px` to `100%`.

**Note:** Since the CSS is minified, class names (like `.Zi`) may change between extension versions. If the script reports "Already fixed or different format" but the fix isn't working, the class name likely changed and the script needs updating.

To find the current class name:
```powershell
(Get-Content "$env:USERPROFILE\.vscode\extensions\anthropic.claude-code-*\webview\index.css" -Raw) -split '}' | Select-String 'max-width:680px'
```

## Compatibility

- Tested with Claude Code extension version 2.1.1
- Windows only (PowerShell scripts)

## License

Apache-2.0
