# Gitpod

Once you add your public ssh key https://gitpod.io/keys you can connect to the
workspace with ssh, find ssh command on three dots Connect via SSH
```
ssh 'duleorlovic-gitpod-gus37vjmteu@duleorlovic-gitpod-gus37vjmteu.ssh.ws-eu64.gitpod.io'
```
and you can mount folder also:
```
sshfs 'duleorlovic-gitpod-gus37vjmteu@duleorlovic-gitpod-gus37vjmteu.ssh.ws-eu64.gitpod.io:/workspace/gitpod' ~/gitpod/  -ocache=no -onolocalcaches -ovolname=ssh

umount -f ~/gitpod
```

Inside VSCODE you can enable extension VCDodeVim https://github.com/VSCodeVim/Vim
You need to paste content to `settings.yml` so using jj will ESC from insert
mode
```
# settings.yml
"vim.insertModeKeyBindings": [
    {
      "before": ["j", "j"],
      "after": ["<Esc>"]
    }
  ],
```

also find some shortcuts when clicking on Gear icon and `Keyboard shortcuts`

Gitpodify

https://www.gitpod.io/guides/gitpodify
* `gp sync` make terminal wait another terminal to complete
* `gp init -i` generate .gitpod.yml file

https://www.gitpod.io/guides/gitpodify#redis
To add redis use custom image
```
# .gitpod.dockerfile
FROM gitpod/workspace-full

# Install Redis.
RUN sudo apt-get update \
 && sudo apt-get install -y \
  redis-server \
 && sudo rm -rf /var/lib/apt/lists/*
```

or choose from custom images https://github.com/gitpod-io/workspace-images/tree/main
and use in command
```
# .gitpod.yml
tasks:
  - init: redis-server
```
and stop workspace (click on gitpod text on bottom right and search for `Gitpod:
Stop Workspace`).


For github you need to install https://github.com/apps/gitpod-io
To rebuild you need to push to origin repo.
And again open workspace using hash

https://gitpod.io/#https://github.com/duleorlovic/gitpod
https://gitpod.io/#prebuild/https://github.com/duleorlovic/gitpod
