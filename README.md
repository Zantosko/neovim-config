# Neovim Configuration Summary

Config location: `~/.config/nvim/`

---

## Structure

```
init.lua                          -- Entry point: loads core modules, bootstraps lazy.nvim
lua/
  core/
    options.lua                   -- Editor settings
    keymaps.lua                   -- Global keybindings
  plugins/
    alpha.lua                     -- Dashboard / start screen
    autocompletion.lua            -- nvim-cmp + LuaSnip
    bufferline.lua                -- Tab-style buffer bar
    colortheme.lua                -- Nord color scheme
    gitsigns.lua                  -- Git gutter signs
    indent-blankline.lua          -- Indent guides
    lsp.lua                       -- LSP servers via Mason
    lualine.lua                   -- Statusline
    misc.lua                      -- Small standalone plugins
    neotree.lua                   -- File explorer
    none-ls.lua                   -- Formatters & linters (format-on-save)
    telescope.lua                 -- Fuzzy finder
    tree-sitter-manager.lua       -- Syntax highlighting (Tree-sitter)
    vim-tmux-navigator.lua        -- Seamless tmux/nvim pane navigation
```

---

## Plugin Manager

**lazy.nvim** -- auto-bootstrapped from GitHub on first launch.

---

## Editor Options (`core/options.lua`)

| Setting | Value | Notes |
|---|---|---|
| Leader key | `Space` | Set in keymaps.lua |
| Line numbers | Relative | `number` + `relativenumber` |
| Indentation | 4 spaces | `shiftwidth`, `tabstop`, `softtabstop` all 4; `expandtab` on |
| Smart indent | On | `smartindent` + `autoindent` |
| Search | Case-insensitive | Unless uppercase used (`smartcase`) |
| Highlight search | Off | Cleared on `<Esc>` |
| Word wrap | Off | `linebreak` on for when toggled |
| Scroll offset | 4 lines vertical, 8 columns horizontal | |
| Mouse | Enabled (all modes) | |
| Clipboard | System (`unnamedplus`) | |
| Undo file | Persistent | `undofile` on |
| Swap/Backup | Disabled | |
| Split direction | Below and right | |
| Sign column | Always visible | |
| Update time | 250ms | |
| Timeout | 300ms | For mapped sequences |
| Mode display | Hidden | Lualine handles it |
| Popup menu height | 10 | |
| Encoding | UTF-8 | |
| Conceallevel | 0 | Backticks visible in markdown |
| Hyphenated words | Treated as one word | `iskeyword` includes `-` |
| Comment auto-insert | Disabled | `formatoptions` removes `c`, `r`, `o` |

---

## Color Theme

**Nord** (`shaunsingh/nord.nvim`) -- loaded first (priority 1000).

- Transparent background enabled by default (`nord_disable_background = true`)
- Contrast enabled, borders disabled, italic/bold disabled
- Toggle transparency: `<leader>bg`
- Lualine theme selectable via `NVIM_THEME` env var (defaults to `nord`, also supports `onedark`)

---

## Key Bindings

Leader key: **Space**

### General

| Keys | Mode | Action |
|---|---|---|
| `<Esc>` | Normal | Clear search highlights |
| `<C-s>` | Normal | Save file |
| `<leader>sn` | Normal | Save without auto-formatting |
| `<C-q>` | Normal | Quit |
| `x` | Normal | Delete char (no register yank) |
| `jk` or `jj` | Insert | Exit insert mode |
| `<Enter>` | Normal | Add blank line below |
| `<Shift-Enter>` | Normal | Add blank line above |
| `<leader>lw` | Normal | Toggle line wrapping |
| `<leader>bg` | Normal | Toggle background transparency |
| `<leader>j` | Normal | Replace word under cursor (incremental `cgn`) |

### Clipboard

| Keys | Mode | Action |
|---|---|---|
| `<leader>y` | Normal/Visual | Yank to system clipboard |
| `<leader>Y` | Normal | Yank entire line to system clipboard |
| `p` | Visual | Paste without losing register |

### Navigation & Scrolling

| Keys | Mode | Action |
|---|---|---|
| `j` / `k` | Normal | Move through wrapped lines visually |
| `<C-d>` / `<C-u>` | Normal | Half-page scroll + center |
| `n` / `N` | Normal | Next/prev search result + center |
| `<C-h/j/k/l>` | Normal | Navigate between splits (also tmux panes) |
| `<C-\\>` | Normal | Navigate to previous tmux pane |

### Buffers

| Keys | Mode | Action |
|---|---|---|
| `<Tab>` | Normal | Next buffer |
| `<Shift-Tab>` | Normal | Previous buffer |
| `<leader>x` | Normal | Close buffer (Bdelete) |
| `<leader>b` | Normal | New empty buffer |

### Windows

| Keys | Mode | Action |
|---|---|---|
| `<leader>v` | Normal | Vertical split |
| `<leader>h` | Normal | Horizontal split |
| `<leader>se` | Normal | Equalize split sizes |
| `<leader>xs` | Normal | Close current split |
| `<leader>n` | Normal | Jump to left window (e.g. Neo-tree) |
| `<leader>m` | Normal | Jump to right window (e.g. file buffer) |
| `<Up/Down>` | Normal | Resize horizontal (+/- 2) |
| `<Left/Right>` | Normal | Resize vertical (+/- 2) |

### Tabs

| Keys | Mode | Action |
|---|---|---|
| `<leader>to` | Normal | New tab |
| `<leader>tx` | Normal | Close tab |
| `<leader>tn` | Normal | Next tab |
| `<leader>tp` | Normal | Previous tab |

### Increment/Decrement

| Keys | Mode | Action |
|---|---|---|
| `<leader>+` | Normal | Increment number |
| `<leader>-` | Normal | Decrement number |

### Visual Mode

| Keys | Mode | Action |
|---|---|---|
| `<` / `>` | Visual | Indent/outdent (stays in visual) |
| `<Alt-j>` | Visual | Move selection down |
| `<Alt-k>` | Visual | Move selection up |

### Diagnostics

| Keys | Mode | Action |
|---|---|---|
| `[d` / `]d` | Normal | Prev/next diagnostic |
| `<leader>d` | Normal | Open floating diagnostic |
| `<leader>q` | Normal | Open diagnostics list (loclist) |
| `<leader>do` | Normal | Toggle all diagnostics on/off |

### Sessions

| Keys | Mode | Action |
|---|---|---|
| `<leader>ss` | Normal | Save session to `.session.vim` |
| `<leader>sl` | Normal | Load session from `.session.vim` |

### LSP (active when a server attaches)

| Keys | Action |
|---|---|
| `gd` | Go to definition (via Telescope) |
| `gr` | Find references (via Telescope) |
| `gI` | Go to implementation |
| `gD` | Go to declaration |
| `K` | Hover documentation |
| `<leader>D` | Type definition |
| `<leader>ds` | Document symbols |
| `<leader>ws` | Workspace symbols |
| `<leader>rn` | Rename symbol |
| `<leader>ca` | Code action |
| `<leader>wa` | Add workspace folder |
| `<leader>wr` | Remove workspace folder |
| `<leader>wl` | List workspace folders |
| `<leader>th` | Toggle inlay hints |

### Telescope (Fuzzy Finder)

| Keys | Action |
|---|---|
| `<leader>sf` | Search files |
| `<leader>sg` | Live grep |
| `<leader>sw` | Grep current word |
| `<leader>sb` or `<leader><leader>` or `<leader><tab>` | Search buffers |
| `<leader>sh` | Search help tags |
| `<leader>sd` | Search diagnostics |
| `<leader>sm` | Search marks |
| `<leader>so` | Search recent files |
| `<leader>sr` | Resume last search |
| `<leader>sds` | Search document symbols (classes, functions, etc.) |
| `<leader>s/` | Live grep in open files only |
| `<leader>/` | Fuzzy find in current buffer |
| `<leader>gf` | Search git files |
| `<leader>gc` | Search git commits |
| `<leader>gcf` | Search git commits for current file |
| `<leader>gb` | Search git branches |
| `<leader>gs` | Search git status |

**Telescope internal mappings:**

- Insert: `<C-j>`/`<C-k>` to move, `<C-l>` to open
- Normal: `q` to close

### Neo-tree (File Explorer)

| Keys | Action |
|---|---|
| `<leader>e` | Toggle tree (left sidebar) |
| `<leader>w` | Toggle tree (floating) |
| `<leader>ngs` | Open git status (floating) |
| `<leader>nf` | Focus tree |
| `\` | Reveal current file in tree |

**Inside Neo-tree:**

| Key | Action |
|---|---|
| `l` or `<CR>` | Open file |
| `S` / `s` | Open in split / vsplit |
| `t` | Open in new tab |
| `w` | Open with window picker |
| `P` | Toggle preview (float) |
| `a` / `A` | Add file / directory |
| `d` | Delete |
| `r` | Rename |
| `y` / `x` / `p` | Copy / cut / paste |
| `c` / `m` | Copy to / move to |
| `C` | Close node |
| `z` | Close all nodes |
| `H` | Toggle hidden files |
| `/` | Fuzzy finder |
| `q` | Close tree |
| `R` | Refresh |
| `o` + `c/d/g/m/n/s/t` | Order by created/diagnostics/git/modified/name/size/type |

### Autocompletion (nvim-cmp)

| Keys | Mode | Action |
|---|---|---|
| `<C-j>` / `<C-k>` | Insert | Navigate completion items |
| `<Tab>` / `<Shift-Tab>` | Insert | Navigate items or jump snippet |
| `<CR>` | Insert | Confirm selection |
| `<C-c>` | Insert | Trigger completion manually |
| `<C-l>` / `<C-h>` | Insert/Select | Jump forward/back in snippet |

---

## LSP Servers

Managed by **Mason** + **mason-lspconfig** + **mason-tool-installer**. Servers are configured with `vim.lsp.config()` + `vim.lsp.enable()`.

| Server | Language |
|---|---|
| `lua_ls` | Lua (configured for Neovim: LuaJIT runtime, vim global) |
| `pylsp` | Python (all built-in plugins disabled -- Ruff handles linting/formatting) |
| `ruff` | Python (linting + formatting) |
| `jsonls` | JSON |
| `sqlls` | SQL |
| `terraformls` | Terraform |
| `yamlls` | YAML |
| `bashls` | Bash / Shell |
| `dockerls` | Dockerfile |
| `docker_compose_language_service` | Docker Compose |
| `html` | HTML (also twig, hbs) |

**LSP features:**
- Cursor-hold reference highlighting (auto-clears on move)
- Inlay hints (toggleable with `<leader>th`)
- LSP status shown via **fidget.nvim**

---

## Formatting & Linting (none-ls / null-ls)

**Format-on-save** is enabled globally via `BufWritePre` autocmd.

| Tool | Purpose | Filetypes |
|---|---|---|
| `prettier` | Formatter | HTML, JSON, YAML, Markdown |
| `stylua` | Formatter | Lua |
| `shfmt` | Formatter | Shell (4-space indent) |
| `terraform_fmt` | Formatter | Terraform |
| `ruff` | Formatter + import sorting | Python (`--extend-select I`) |
| `ruff_format` | Formatter | Python |
| `eslint_d` | Linter | JS/TS |
| `checkmake` | Linter | Makefiles |

**StyLua config** (`.stylua.toml`): 160 col width, 2-space indent, single quotes, Unix line endings, no call parentheses.

Use `<leader>sn` to save without triggering auto-format.

---

## Autocompletion

**nvim-cmp** with sources (in priority order):

1. LSP (`nvim_lsp`)
2. Snippets (`luasnip` -- VSCode-style via `friendly-snippets`)
3. Buffer words
4. File paths

Completion items show kind icons and source labels (`[LSP]`, `[Snippet]`, `[Buffer]`, `[Path]`).

---

## Tree-sitter

**tree-sitter-manager.nvim** -- lightweight manager for parser installation. Highlighting enabled, auto-install off. Parsers stored in `~/.local/share/nvim/site/parser/`.

---

## UI Components

| Component | Plugin | Notes |
|---|---|---|
| Statusline | lualine.nvim | OneDark-style colors, shows mode/branch/filename/diagnostics/diff/encoding/filetype/location/progress. Hidden for alpha, neo-tree, Avante filetypes. |
| Buffer bar | bufferline.nvim | Tab-like buffer display with `vim-bbye` for clean close. Sorted by insertion order. `│` separators. |
| Indent guides | indent-blankline.nvim | Thin `▏` character, scope markers disabled. |
| Dashboard | alpha-nvim | Startify theme with NEOVIM ASCII art header. |
| Git gutter | gitsigns.nvim | `+` add, `~` change, `_` delete, `‾` topdelete. |
| File icons | nvim-web-devicons | Used by neo-tree, bufferline, telescope, lualine. |
| Which-key | which-key.nvim | Keybind hints popup (3 second delay). |
| Color highlighter | nvim-colorizer.lua | Inline color preview for hex codes, etc. |
| Todo highlights | todo-comments.nvim | Highlights TODO, NOTE, etc. in comments. |

---

## Other Plugins

| Plugin | Purpose |
|---|---|
| nvim-autopairs | Auto-close brackets, quotes, etc. |
| nvim-ts-autotag | Auto-close/rename HTML tags |
| vim-sleuth | Auto-detect indentation from file |
| vim-fugitive | Git commands (`:Git`, `:Gblame`, etc.) |
| vim-rhubarb | GitHub integration for fugitive (`:GBrowse`) |
| vim-tmux-navigator | `<C-h/j/k/l>` moves between nvim splits and tmux panes seamlessly |

---

## Neo-tree File Explorer Details

- Position: left sidebar, 40 columns wide
- Dotfiles: shown (hidden files visible)
- Hidden by name: `.DS_Store`, `thumbs.db`, `node_modules`, `__pycache__`, `.virtual_documents`, `.git`, `.python-version`, `.venv`
- Git status icons: `✖` deleted, `󰁕` renamed, `` untracked, `` ignored, `󰄱` unstaged, `` staged, `` conflict
- Replaces netrw (`hijack_netrw_behavior = 'open_default'`)
- Git status window opens as float with stage/unstage/commit/push commands

---

## Tmux Integration

`vim-tmux-navigator` maps `<C-h/j/k/l>` to navigate seamlessly between Neovim splits and tmux panes. `<C-\\>` goes to the previous tmux pane.
