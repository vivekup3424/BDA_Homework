Here is the properly formatted version of your instructions:

# Hadoop Setup Instructions

## 1. Create a New User on the Linux Machine

```bash
sudo adduser hadoop # I have provided the password "hadoop"
```

You can leave the rest of the user data empty. Simply skip over the fields by pressing `Enter` continuously.

## 2. Log in as the Hadoop User

```bash
su - hadoop
```

### `su (switch user)`
The `-`, `-l`, or `--login` options start the shell as a login shell with an environment similar to a real login:

- Clears all environment variables except `TERM` and variables specified by `--whitelist-environment`.
- Initializes the environment variables `HOME`, `SHELL`, `USER`, `LOGNAME`, and `PATH`.
- Changes to the target user’s home directory.
- Sets `argv[0]` of the shell to `'-'` to make the shell a login shell.
