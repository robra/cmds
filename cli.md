# Bash Basics
## Print environment variables
```zsh
 printenv
```

## Set environment variable for current session
```zsh
export VAR_NAME="value"
```

## Apply changes via sourcing
```zsh
source ~/.zshrc
```

## Permanent as part of startup script
```zsh
echo 'export VAR_NAME="value"' >> ~/.zshrc
```

## Show the size of a folder
```zsh
du -sh FOLDER
```