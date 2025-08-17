# Nushell builtins
- `complete -h` - 

# Searching files/directories
- `fd --hidden . ~ | fzf` - Look for all files (including hidden) starting at ~home directory
- `fd --type f . | fzf` - Only search files (skip directories)
- `fd --type d . | fzf` - Only search directories
- `fd -i . | fzf` - Case insensitive search
- `nvim (fd . ~ | fzf)` - Open up search with neovim
- `y (fd . ~ | fzf)` - Open up search with yazi
- `xdg-open (fd . ~ | fzf)` - Open up search with xdg-open (probably prefer yazi other than this)
- ``
