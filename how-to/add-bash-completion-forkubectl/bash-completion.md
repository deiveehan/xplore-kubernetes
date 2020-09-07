### Getting started
It may be difficult to remember all the commands, fortunately you can use the bash completion to use tab to find out all the commands

```shell script
alias k=kubectl

k version
```
#### Bash completion
Ensure you have the latest version of bash running atleast 4.1 + 

Reference: https://kubernetes.io/docs/tasks/tools/install-kubectl/

```shell script
brew install bash-completion@2
```

Add the following in the .bashrc folder
```shell script
export BASH_COMPLETION_COMPAT_DIR="/usr/local/etc/bash_completion.d"
[[ -r "/usr/local/etc/profile.d/bash_completion.sh" ]] && . "/usr/local/etc/profile.d/bash_completion.sh"

source <(kubectl completion bash | sed s/kubectl/k/g)
alias k=kubectl

complete -F __start_kubectl k
```
Your auto completion using the tab should work after this change. 


