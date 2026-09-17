# SSH multiplexing on Bunya

## Quick links

- [What is SSH multiplexing?](#what-is-ssh-multiplexing)
- [Before you start](#before-you-start)
- [Which computers can use it?](#which-computers-can-use-it)
- [Setting it up (Mac, Linux and WSL)](#setting-it-up-mac-linux-and-wsl)
- [Using it](#using-it)
- [Checking and closing the shared connection](#checking-and-closing-the-shared-connection)
- [PuTTY users](#putty-users)
- [Troubleshooting](#troubleshooting)

## What is SSH multiplexing?

Each time you run `ssh`, `scp`, `sftp` or `rsync` to Bunya, your computer normally opens a new connection and you must enter your password and your MFA code again.

SSH multiplexing lets you log in once. Your first connection stays open, and any further `ssh`, `scp`, `sftp` or `rsync` commands to Bunya use that same connection. You are not asked for your password or MFA code again while the first connection is open.

This is useful if you:

- work in several terminal windows on Bunya at the same time
- copy files with many separate `scp` or `rsync` commands
- run scripts on your own computer that connect to Bunya more than once

All sessions that share a connection are on the same Bunya login node as your first session. Use the `hostname` command to see which login node you are on.

## Before you start

> [!CAUTION]
> ***While the shared connection is open, anyone who can use your local account on your computer can open a session on Bunya as you, without a password or MFA code.***
>
> Only set this up on a computer where you have your own local account that nobody else uses.
> Lock your screen when you step away from your computer.
> Close the shared connection when you have finished working (see [below](#checking-and-closing-the-shared-connection)).
>
> The rules in the [Bunya User Guide](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#connecting) about not sharing passwords, SSH keys or MFA apply here too. Allowing another person to use your shared connection is a violation of UQ's policies and the Bunya conditions of access.

## Which computers can use it?

| Your computer | Can use multiplexing? |
| ------------- | --------------------- |
| Mac | Yes, using Terminal |
| Linux | Yes |
| Windows with WSL | Yes, from inside WSL |
| Windows `cmd` or PowerShell | No. The SSH client built into Windows does not support multiplexing. Please use WSL. |
| Windows with PuTTY | Yes, using PuTTY's own setting. See [PuTTY users](#putty-users). |
| Windows with WinSCP | Not needed. WinSCP already lets you transfer many files after a single MFA login. |
| Windows with MobaXterm | No. MobaXterm does not support multiplexing.

## Setting it up (Mac, Linux and WSL)

All of these steps are done on **your own computer**, not on Bunya.

### Step 1: Create a folder for the connection files

```
mkdir -p ~/.ssh/sockets
chmod 700 ~/.ssh ~/.ssh/sockets
```

### Step 2: Add Bunya to your SSH config file

Open the file `~/.ssh/config` in a text editor (create it if it does not exist) and add the following lines.
Replace `username` with your Bunya username. UQ users use their UQ username. QCIF users use their QSAC username.

```
Host bunya
    HostName bunya.rcc.uq.edu.au
    User username
    ControlMaster auto
    ControlPath ~/.ssh/sockets/%C
    ControlPersist 1h
    ServerAliveInterval 60
    ServerAliveCountMax 3
```

Then make sure only you can read the file:

```
chmod 600 ~/.ssh/config
```

> [!NOTE]
> If your `~/.ssh/config` file already has a `Host *` section, put the `Host bunya` lines **above** it. SSH uses the first value it finds for each setting. Or use a unique name instead of `bunya` to distinguish from a non-multiplexing connection.

### What these lines do

| Setting | What it does |
| ------- | ------------ |
| `Host bunya` | A short name for Bunya. You can now type `ssh bunya` instead of `ssh username@bunya.rcc.uq.edu.au` |
| `HostName` | The address of Bunya |
| `User` | Your Bunya username |
| `ControlMaster auto` | Use the shared connection if one is open. If none is open, start one. |
| `ControlPath` | Where the shared connection file is kept. `%C` is replaced with a unique code made from your connection details. |
| `ControlPersist 1h` | Keep the shared connection open for 1 hour after your last session to Bunya closes |
| `ServerAliveInterval 60` and `ServerAliveCountMax 3` | Check every 60 seconds that Bunya can still be reached. Close the shared connection after 3 checks with no reply (about 3 minutes). |

You can make `ControlPersist` shorter (for example `15m`) if you prefer. A shorter time means you will be asked to log in again more often.

## Using it

> [!IMPORTANT]
> Always use the short name `bunya` in your commands.
> If you type the full address, for example `ssh username@bunya.rcc.uq.edu.au`, the settings above are not used and you will be asked for your password and MFA code every time.

### Log in the first time

```
ssh bunya
```

Enter your password and MFA code as normal. See the [MFA section of the Bunya User Guide](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#bunya-enforces-mfa-multi-factor-authentication) if you need help with this step.

### Open more sessions

Open another terminal window on your computer and type:

```
ssh bunya
```

You will be logged in straight away, with no password or MFA prompt.

### Copy files

Copy a file from your computer to your Bunya scratch directory:

```
scp results.tar.gz bunya:/scratch/user/username/
```

Copy a file from Bunya to the current folder on your computer:

```
scp bunya:/scratch/user/username/output.log .
```

Copy a whole folder with `rsync`:

```
rsync -av mydata/ bunya:/scratch/user/username/mydata/
```

Start an `sftp` session:

```
sftp bunya
```

None of these commands will ask for your password or MFA code while the shared connection is open.

## Checking and closing the shared connection

### Is the shared connection open?

```
ssh -O check bunya
```

If it is open you will see something like:

```
Master running (pid=12345)
```

### Close the shared connection

```
ssh -O exit bunya
```

You will see:

```
Exit request sent.
```

> [!WARNING]
> `ssh -O exit bunya` closes **every** session that uses the shared connection. This includes any `scp`, `sftp` or `rsync` transfer that is still running. Wait for your transfers to finish first.

If you close the terminal window you used for your first login, the shared connection stays open in the background until the `ControlPersist` time runs out. Your other sessions keep working.

## PuTTY users

PuTTY has its own connection sharing setting.

1. Open PuTTY and load (or create) your saved session for `bunya.rcc.uq.edu.au`.
2. In the left menu go to *Connection ... SSH*.
3. Tick **Share SSH connections if possible**.
4. Go back to *Session* and click **Save**.

Log in with this saved session as normal. Any further PuTTY windows opened with the same saved session will log in without asking for your password or MFA code.

Keep the first PuTTY window open. Closing it ends the other PuTTY sessions that share its connection.

## Troubleshooting

### I am still asked for my password and MFA code

- Check that you typed `ssh bunya` and not the full address.
- Check that the `Host bunya` section is above any `Host *` section in `~/.ssh/config`.
- Check that you are using Mac, Linux or WSL. The Windows `cmd` and PowerShell SSH client does not support multiplexing.

### `ssh bunya` hangs, or gives an error about the control socket

This can happen after your computer has been asleep, after you change network, or after your VPN disconnects.

1. Run `ssh -O exit bunya`.
2. If that does not work, delete the connection files and log in again:

```
rm -f ~/.ssh/sockets/*
ssh bunya
```

### Bunya maintenance days

Bunya is taken offline for maintenance on the second Tuesday of February, May, August and November. Your shared connection will be closed. Log in again once Bunya is back. See [When Bunya is down for maintenance](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#when-bunya-is-down-for-maintenance).

### I want a separate connection that does not use the shared one

```
ssh -S none bunya
```

This opens a new, independent connection. You will be asked for your password and MFA code.

### Still stuck?

Email <rcc-support@uq.edu.au> and include:

- your Bunya username
- where you are connecting from (e.g. campus, home, VPN)
- your operating system and the tool you are using (e.g. Mac Terminal, WSL, PuTTY)
- the output of `ssh -v bunya`
