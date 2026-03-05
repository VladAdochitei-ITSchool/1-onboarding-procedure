# Procedura Onboarding Github
Procedura de onboarding a cursantilor pentru mediul de Github.

> Referinte:
> - https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent?platform=linux
> - https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account
> - https://www.markdownguide.org/extended-syntax/

## Pasul 1
Se genereaza o cheie noua ssh cu comanda: 

```sh
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Ulterior vom avea o pereche de chei local in folderul in care am rulat comanda:

```
.
├── github_access_key
└── github_access_key.pub

1 directory, 2 files
```

> 📍 Cheia `.pub` va fi adaugata in contul de `Github` iar cheia fara extensie este cea privata, care va fi adaugata in *agentul de ssh* (local pe workstation)

## Pasul 2
Mutam cheia privata din locul in care am initializat-o in locul destinat stocarii cheilor ssh:

```sh
mv github_access_key ~/.ssh
```

## Pasul 3 
Se initializeaza daemonul de agent ssh:

```sh
$ eval "$(ssh-agent -s)"
> Agent pid 59566
```

Se adauga cheia privata in agentul de ssh:

```sh
ssh-add ~/.ssh/github_access_key
```

---

## SSH configuration file for Github and other SSH server accesss

```
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/github_private_key
  IdentitiesOnly yes
```
