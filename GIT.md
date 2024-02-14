# Git

```shell
sudo apt update && sudo apt upgrade
```

```shell
sudo apt-get install git
```

```shell
git config --global user.name "Your Name"
```

```shell
git config --global user.email "youremail@domain.com"
```

```shell
ssh-keygen -t ed25519 -C "your_email@example.com"
```

```shell
eval "$(ssh-agent -s)"
```

```shell
ssh-add ~/.ssh/id_ed25519
```

```shell
ssh -T git@github.com
```

## Bitbucket config

```
Host bitbucket.org
  AddKeysToAgent yes
  IdentityFile ~\.ssh\id_ed25519
```
