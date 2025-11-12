# Overview

This document provides the initial environment setup required for working with this organization (e.g., `llamandcoco`).
It covers the installation and configuration of essential tools for daily development, including shell productivity plugins, AWS SSO access, and Terraform version management.

Tools covered:

- [oh-my-zsh](https://github.com/ohmyzsh/ohmyzsh) and recommended plugins
- [aws-vault](https://github.com/99designs/aws-vault) (for secure AWS Identity Center / SSO login)
- [tfenv](https://github.com/tfutils/tfenv) (Terraform version manager)

## oh-my-zsh

### Install oh-my-zsh

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### Install Plugins

zsh-autosuggestions

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

fast-syntax-highlighting

```bash
git clone https://github.com/zdharma-continuum/fast-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/fast-syntax-highlighting
```

zsh-autocomplete

```bash
git clone --depth 1 https://github.com/marlonrichert/zsh-autocomplete.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autocomplete
```

Update `.zshrc`.

```bash
vim ~/.zshrc
```

Modify the plugins section:

```bash
plugins=(
  git
  zsh-autosuggestions
  fast-syntax-highlighting
  zsh-autocomplete
)
```

Apply the changes:

```bash
source ~/.zshrc 
```

## Install aws-vault

### Install 

```bash
brew install aws-vault
```

### Configure AWS Identity Center (SSO)

Manually edit the AWS config file:

```bash
vim ~/.aws/config
```

Add your SSO profile:

```ini
[profile <PROFILE_NAME>]
sso_start_url  = https://<your-org>.awsapps.com/start
sso_region     = <aws-region>   # Region where Identity Center is hosted
sso_account_id = <account-id>
sso_role_name  = <role-name>
region         = <aws-region>   # Default AWS CLI region for resources
```

> [!tip]
> `sso_region` and `region` serve different purposes, and both are required.

### Test login

```bash
aws-vault login <PROFILE_NAME>
```

## tfenv

### Install

```bash
brew install tfenv
```

### Install and use a specific Terraform version

```bash
tfenv install 1.13.5
tfenv use 1.13.5
```
