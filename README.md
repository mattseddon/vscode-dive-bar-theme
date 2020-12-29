# A dark theme which will making your VSCode session look like the inside of a dive bar.

## What it looks like

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

### Bracket Pair Colorizer 2

If you already use the Bracket Pair Colorizer
you can match the bracket colors to the rest of this theme:

```json
{
  "bracket-pair-colorizer-2.colors": ["#0adb8b", "#00eaff", "#f60e67"]
}
```

### Integrated Terminal

For your terminal it is recommended to use the [Powerlevel10k][] terminal
theme with the `MesloLGS NF` font:

```json
{
  "terminal.integrated.fontFamily": "MesloLGS NF"
}
```

[powerlevel10k]: https://github.com/romkatv/powerlevel10k

If you chose to use p10k then you should overwrite the my_git_formatter
function in your .p10k.zsh with the following:

```bash
  function my_git_formatter() {
    emulate -L zsh

    if [[ -n $P9K_CONTENT ]]; then
      typeset -g my_git_format=$P9K_CONTENT
      return
    fi

    if (( $1 )); then
      local       meta='%f'     # default foreground
      local      clean='%41F'   # story maps green foreground
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
