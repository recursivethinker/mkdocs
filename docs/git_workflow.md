# My git workflow

## Setup env vars.

```
github_username=<your_github_username>
```

```
repository=<your_repository>
```

## Clone the repo.
```
git clone https://github.com/$github_username/$repository.git
```

## Check status.

```
cd $repository
```

```
git status
```

## Checkout a new branch for development.

```
git checkout -b new-feature-branch
```

## Config.

List all git configs

```
git config --list
```

Change local git username and email.

```
git config --local user.name "username"
```

```
git config --local user.email "email"
```

## Push changes to origin

```
git push origin main
```

Typically I need a username and password to do this. I use a Personal Access
Token (PAT) from git. [Managing Personal Access
Tokens](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)

I save them in my pass db and use the following to retrieve them.

```
pass show github/username -c

pass show github/pat -c
```
