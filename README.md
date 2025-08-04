# A dark theme which makes Visual Studio Code look like the inside of a dive bar.

## How it looks

### Python

<div align="center">
  <img
    src="https://raw.githubusercontent.com/mattseddon/vscode-dive-bar-theme/main/images/Python.png"
    role="presentation"
  />
</div>

### TypeScript

<div align="center">
  <img
    src="https://raw.githubusercontent.com/mattseddon/vscode-dive-bar-theme/main/images/TypeScript.png"
    role="presentation"
  />
</div>

## Some extra configuration

### Bracket Pair Colorization

Bracket pair colorization is now a native feature in VS Code.
This theme has colors set for bracket pairs by default.
In order to enable set the following options:

```json
{
    "editor.bracketPairColorization.enabled": true,
    "editor.guides.bracketPairs": "active"
}
```

If you use a version of VS Code from before 1.60.0 and/or still want
to use Bracket Pair Colorizer 2 you can match the bracket colors to the rest of this theme:

```json
{
    "bracket-pair-colorizer-2.colors": ["#0adb8b", "#00eaff", "#f60e67"]
}
```

### Coverage Gutters

Set the following options in your config to update the colors of the gutters provided by Coverage Gutters to match this theme:

```json
{
    "coverage-gutters.highlightdark": "rgba(10, 219, 139, 1)",
    "coverage-gutters.noHighlightDark": "rgba(246, 14, 103, 1)",
    "coverage-gutters.partialHighlightDark": "rgba(0, 234, 255, 1)",
    "coverage-gutters.showLineCoverage": false
}
```

### Git Graph

If you use Git Graph the following settings will match the rest of this theme:

```json
{
    "git-graph.graph.colours": [
        "#FF428E",
        "#A8FFEF",
        "#0ADB8B",
        "#00EAFF",
        "#F834BB",
        "#2BF5E9",
        "#D831D7",
        "#FF594C"
    ]
}
```

### Import Costs

If you are using the Import Costs extension these settings will
match the rest of this theme:

```json
{
    "importCost.smallPackageColor": "#0adb8b",
    "importCost.mediumPackageColor": "#00eaff",
    "importCost.largePackageColor": "#f60e67"
}
```

### Integrated Terminal

For your terminal it is recommended that you use [Powerlevel10k][]
for `zsh` with the `MesloLGS NF` font:

```json
{
    "terminal.integrated.fontFamily": "MesloLGS NF"
}
```

[powerlevel10k]: https://github.com/romkatv/powerlevel10k

If you chose to use `Powerlevel10k` then you should overwrite the
`my_git_formatter` function in your `.p10k.zsh` with the following:

```bash
  function my_git_formatter() {
    emulate -L zsh

    if [[ -n $P9K_CONTENT ]]; then
      typeset -g my_git_format=$P9K_CONTENT
      return
    fi

    if (( $1 )); then
      local       meta='%f'     # default foreground
      local      clean='%41F'   # green foreground
      local   modified='%45F'   # blue foreground
      local  untracked='%001F'  # red foreground
      local conflicted='%001F'  # red foreground
    else
      local       meta='%244F'  # grey foreground
      local      clean='%244F'  # grey foreground
      local   modified='%244F'  # grey foreground
      local  untracked='%244F'  # grey foreground
      local conflicted='%244F'  # grey foreground
    fi

    local res
    local where  # branch or tag
    if [[ -n $VCS_STATUS_LOCAL_BRANCH ]]; then
      res+="${clean}${(g::)POWERLEVEL9K_VCS_BRANCH_ICON}"
      where=${(V)VCS_STATUS_LOCAL_BRANCH}
    elif [[ -n $VCS_STATUS_TAG ]]; then
      res+="${meta}#"
      where=${(V)VCS_STATUS_TAG}
    fi

    (( $#where > 32 )) && where[13,-13]="…"
    res+="${clean}${where//\%/%%}"  # escape %

    [[ -z $where ]] && res+="${meta}@${clean}${VCS_STATUS_COMMIT[1,8]}"

    if [[ -n ${VCS_STATUS_REMOTE_BRANCH:#$VCS_STATUS_LOCAL_BRANCH} ]]; then
      res+="${meta}:${clean}${(V)VCS_STATUS_REMOTE_BRANCH//\%/%%}"  # escape %
    fi

    (( VCS_STATUS_COMMITS_BEHIND )) && res+=" ${clean}⇣${VCS_STATUS_COMMITS_BEHIND}"
    (( VCS_STATUS_COMMITS_AHEAD && !VCS_STATUS_COMMITS_BEHIND )) && res+=" "
    (( VCS_STATUS_COMMITS_AHEAD  )) && res+="${clean}⇡${VCS_STATUS_COMMITS_AHEAD}"
    (( VCS_STATUS_PUSH_COMMITS_BEHIND )) && res+=" ${clean}⇠${VCS_STATUS_PUSH_COMMITS_BEHIND}"
    (( VCS_STATUS_PUSH_COMMITS_AHEAD && !VCS_STATUS_PUSH_COMMITS_BEHIND )) && res+=" "
    (( VCS_STATUS_PUSH_COMMITS_AHEAD  )) && res+="${clean}⇢${VCS_STATUS_PUSH_COMMITS_AHEAD}"
    (( VCS_STATUS_STASHES        )) && res+=" ${clean}*${VCS_STATUS_STASHES}"
    [[ -n $VCS_STATUS_ACTION     ]] && res+=" ${conflicted}${VCS_STATUS_ACTION}"
    (( VCS_STATUS_NUM_CONFLICTED )) && res+=" ${conflicted}~${VCS_STATUS_NUM_CONFLICTED}"
    (( VCS_STATUS_NUM_STAGED     )) && res+=" ${modified}+${VCS_STATUS_NUM_STAGED}"
    (( VCS_STATUS_NUM_UNSTAGED   )) && res+=" ${modified}!${VCS_STATUS_NUM_UNSTAGED}"
    (( VCS_STATUS_NUM_UNTRACKED  )) && res+=" ${untracked}${(g::)POWERLEVEL9K_VCS_UNTRACKED_ICON}${VCS_STATUS_NUM_UNTRACKED}"
    (( VCS_STATUS_HAS_UNSTAGED == -1 )) && res+=" ${modified}─"

    typeset -g my_git_format=$res
  }
```
