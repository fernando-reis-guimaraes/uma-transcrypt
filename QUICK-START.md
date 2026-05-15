# Quick Start (uma-transcrypt)

Use this fork with the `uma-transcrypt` command.

## 1) Validate your environment

Required tools:

- Bash
- Git
- OpenSSL

Optional but recommended before production rollout:

```bash
shellcheck transcrypt uma-transcrypt
/tmp/bats-core/bin/bats tests/
```

## 2) Install command

From the repository root:

```bash
sudo install -m 0755 uma-transcrypt /usr/local/bin/uma-transcrypt
```

## 3) Set password via environment variable

```bash
export TRANSCRYPT_PASSWORD='change-me'
```

For named contexts, use:

```bash
export TRANSCRYPT_PASSWORD_SUPER_SECRET='change-me-too'
```

## 4) Initialize and verify

Inside your Git repository:

```bash
uma-transcrypt --cipher=aes-256-cbc --yes
uma-transcrypt --display
```

Verify helper scripts and hooks were installed:

```bash
test -x .git/crypt/transcrypt
test -x .git/hooks/pre-commit
test -x .git/hooks/pre-commit-crypt
```

## 5) Encrypt files

```bash
uma-transcrypt --add sensitive_file
git add .gitattributes sensitive_file
git commit -m "Add encrypted sensitive_file"
```

## Production notes

- `uma-transcrypt` is the fork entrypoint; `transcrypt` remains as compatibility.
- Git filters and hooks execute `.git/crypt/transcrypt`, which is installed during init.
- Validate in a staging clone first, then roll out to production repositories.
