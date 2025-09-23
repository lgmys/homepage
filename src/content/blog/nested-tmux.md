---
title: 'Less painful nested Tmux'
description: 'Some notes on how to tackle nested tmux sessions, to make them easier to work with'
pubDate: 'Sep 23 2025'
heroImage: './nested-tmux-hero.jpg'
---

Recently, I started using the following script to first display a nice `fzf` menu with session names. When a selection is made, it creates a session with a prefix different from the inner tmux one (just local to the "outer" session).

Connecting to an SSH host running tmux and managing it with the top-level multiplexer has become a breeze.

```
create_nested_session() {
  local choice
  choice=$(printf "host a\nhost b\n" | fzf --prompt="Select remote ssh: ")

  if [[ -z "$choice" ]]; then
    echo "No selection made."
    return 1
  fi

  local session_name
  session_name="  [nested] $choice"

  if tmux has-session -t "$session_name" 2>/dev/null; then
    tmux switch-client -t $session_name;
    return 0;
  fi

  tmux new-session -s $session_name -d
  tmux set-option -t $session_name prefix C-b;
  tmux set-option -t $session_name status-left "#[fg=yellow] 󰢹  $choice";
  tmux set-option -t $session_name status-right "Parent prefix: C-b";
  tmux set-option -t $session_name status-position bottom;
  tmux set-option -t $session_name status-justify absolute-centre
  tmux set-option -t $session_name window-status-format ""
  tmux set-option -t $session_name window-status-current-format ""
  tmux send-keys -t $session_name "ssh $choice" C-m
  tmux switch-client -t $session_name
}
```
