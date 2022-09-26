# Gitpod


For github you need to install https://github.com/apps/gitpod-io
To rebuild you need to push to origin repo.
And again open workspace using hash

https://gitpod.io/#https://github.com/duleorlovic/gitpod
https://gitpod.io/#prebuild/https://github.com/duleorlovic/gitpod

# Connect to workspace

Once you add your public ssh key https://gitpod.io/keys you can connect to the
workspace with ssh, find ssh command on three dots and `Connect via SSH` menu
```
ssh 'duleorlovic-gitpod-gus37vjmteu@duleorlovic-gitpod-gus37vjmteu.ssh.ws-eu64.gitpod.io'
```
and you can mount folder also:
```
sshfs 'duleorlovic-gitpod-gus37vjmteu@duleorlovic-gitpod-gus37vjmteu.ssh.ws-eu64.gitpod.io:/workspace/gitpod' ~/gitpod/  -ocache=no -onolocalcaches -ovolname=ssh

umount -f ~/gitpod
```

You can share workspace, but than anyone who has account on gitpod can access
this workspaces. Note to test in new incognito window with new gitpod session.
When you stop sharing user can still see updates live and autosave will work.
But once they reload the page, stoped sharing workspace could not be opened.

## Vim

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

By default create prebuild for master and pullRequests

# Gitpodify

https://www.gitpod.io/guides/gitpodify
`gp` cli command is available inside workspaces.
* `gp sync` make terminal wait another terminal to complete
* `gp init -i` generate .gitpod.yml file

gitpod.yml should define image, tasks and ports
```
# .gitpod.yml
# https://www.gitpod.io/docs/references/gitpod-yml
tasks:
  # each task will start new terminal
  - name: Term 1 # name in sidebar
    before: echo "before script"
    init: bundle install # performed only once when workspace is created
    command: bin/rails s # this is performed when workspace is started/restarted
```


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

# Rails

Add any two level subdomain like asd.123.gitpod.io
```
# config/application.rb
    config.hosts << /.*gitpod.io/
```
