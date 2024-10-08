# live-rename.nvim
A neovim plugin to live preview lsp renames.

https://github.com/user-attachments/assets/7cc03f60-3c59-45f5-b8e7-e53e324ce56b

## Installation
[__lazy.nvim__](https://github.com/folke/lazy.nvim)
```lua
{ "saecki/live-rename.nvim" }
```

[__vim-plug__](https://github.com/junegunn/vim-plug)
```
Plug 'saecki/live-rename.nvim'
```

## Setup (optional)
```lua
-- default config
require("live-rename").setup({
    -- Send a `textDocument/prepareRename` request to the server to
    -- determine the word to be renamed, can be slow on some servers.
    -- Otherwise fallback to using `<cword>`.
    prepare_rename = true,
    request_timeout = 1500,
    keys = {
        submit = {
            { "n", "<cr>" },
            { "v", "<cr>" },
            { "i", "<cr>" },
        },
        cancel = {
            { "n", "<esc>" },
            { "n", "q" },
        },
    },
    hl = {
        current = "CurSearch",
        others = "Search",
    },
})
```

## Usage

```lua
-- start in normal mode and jump to the start of the word
require("live-rename").rename()

-- start in insert mode and jump to the end of the word
require("live-rename").rename({ insert = true })

-- jump into insert mode and start with an empty word
require("live-rename").rename({ text = "", insert = true })
```

live-rename includes a `map` function to make creating key mappings more ergonomic.  
The options accepted are the same as for `rename`.
```lua
-- equivalent
vim.keymap.set("n", "<leader>r", require("live-rename").rename)
vim.keymap.set("n", "<leader>r", require("live-rename").map())
vim.keymap.set("n", "<leader>r", require("live-rename").map({}))

-- equivalent
vim.keymap.set("n", "<leader>R", require("live-rename").map({ text = "", insert = true }))
vim.keymap.set("n", "<leader>R", function() require("live-rename").rename({ text = "", insert = true }) end)
```
