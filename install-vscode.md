[Home](https://github.com/scott-knight/linux-on-windows-11) | [Previous Step](install-wsl2.md) | [Next Step](install-windows-terminal.md)

<br/>

# Install VS Code

You don't actually have to do this step if you prefer using VIM or Nano to edit config files or write code. I prefer using it, therefore recommend installing it. One of the great features of VS Code is the ability to save/sync your VS Code settings to Github.

## Download VS Code

You can download VSCode [from here](https://code.visualstudio.com/Download). Once downloaded, run the install.

## Setup

1. Once installed, click in the user icon in the lower left corner:

![vscode](https://user-images.githubusercontent.com/516548/112903017-97c55a00-90ac-11eb-9077-e9c34b3e8a6f.png)

2. Click `sign in to sync settings`.
3. Select whichever account applies. There will be two options, GitHub and Microsoft. I save my settings to GitHub. In either case, it will open a browser session for you to authenticate into the site. Once authenticated, it will sync down any settings previously saved, including any installed plugins/extensions. Any changes made to VSCode will be synced to your account.

<br/>

## Plugins (Extensions)

If you haven't previously sync'ed/saved settings to Github or Microsoft, here is a handy list of plugins to install:

```txt
Auto Close Tag
Better HAML
Bracket Pair Colorizer 2
Disable ESLint Rule
EditorConfig for VSCode
Erb-types
ESLint
Git
Git Blame
Git Graph
Git History
GitLens
Import Cost
JavaScript ES6 Snippets
Language Stylus
Live Server
Material Icon Theme
Prettier
Rails Edit Credentials
Rails i18n
Ruby
Ruby HAML
Simple Icons
VSCode Database
Markdown All in One
Markdown Converter
Markdown Preview Enhanced
MarkdownLint
Sass
Sublime Comands
Sublime Text Keymap
Slim
Sunburst Theme
TODO Highlight
Pug extension pack
vscode-elixir
XML Tools
Rainbow CSV
Edit csv
Svelte for VSCode
```

After extension are installed, open `preferences > settings`.

<br/>

## Preferences > Settings

To get to the settings click `File > Preferences > Settings`

When the settings open, click the JSON settings icon:

![vscode settings](https://user-images.githubusercontent.com/516548/112904337-69487e80-90ae-11eb-8416-19d0db5ffafe.png)

Below is an example of settings. You can copy/paste any (or all) of these settings to the settings file:

```json
{
  "workbench.startupEditor": "newUntitledFile",
  "workbench.iconTheme": "material-icon-theme",
  "editor.minimap.enabled": false,
  "editor.tabSize": 2,
  "editor.detectIndentation": false,
  "editor.wordWrap": "on",
  "files.trimTrailingWhitespace": true,
  "diffEditor.ignoreTrimWhitespace": false,
  "files.trimFinalNewlines": true,
  "explorer.confirmDelete": false,
  "editor.rulers": [
    120
  ],
  "scss.validate": false,
  "explorer.confirmDragAndDrop": false,
  "gitlens.advanced.messages": {
    "suppressGitMissingWarning": true
  },
"svelte.enable-ts-plugin": true,
"security.workspace.trust.untrustedFiles": "open",
"files.insertFinalNewline": true,
"html.format.endWithNewline": true,
"vscode-edge-devtools.mirrorEdits": true,
"bracket-pair-colorizer-2.depreciation-notice": false,
"workbench.editor.showTabs": true,
"ruby.intellisense": "rubyLocate",
"git.autofetch": true,
"workbench.colorTheme": "Sunburst",
"redhat.telemetry.enabled": false,
"yaml.maxItemsComputed": 200000,
"githubPullRequests.pullBranch": "never",
}
```

Once your account is ready to sync, your extensions are installed and your JSON settings are in place, you are good to go. The next time you install VS Code, simply log in to your account (as previously described) and all the extensions and settings will automatically pull down to yourl local VS Code, saving you a ton of time in setup.

Now you are ready to [Install Windows Termial](install-windows-terminal.md).

<br/>

[Home](https://github.com/scott-knight/linux-on-windows-11) | [Previous Step](install-wsl2.md)
