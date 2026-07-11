---
title: Understanding Environment Variables in Liquid Galaxy
contributor: Sahana K B
date: March 1, 2026
---

# Understanding Environment Variables in Liquid Galaxy

## Category: Rig Side

System-wide configurations that affect the behaviour of programs and services are known as “environment variables”. In Liquid Galaxy configurations, environment variables are used to define execution paths, display settings, and operational parameters.

Use the commands below to view environment variables in your system.

```bash
printenv
```

Additionally, you can display specific environment variable values with commands such as:

```bash
echo $PATH
echo $DISPLAY
```

The value stored in the PATH environment variable tells the system where to look for executables when you run a command. If the PATH environment variable doesn’t include the required locations of executables, the system will not recognize commands, and they will fail.

The DISPLAY environment variable tells a graphical application where to display graphical output. When you launch a graphical application (like Chromium), the application will check the value of the DISPLAY environment variable to determine where to display output.

To temporarily create an environment variable, use the `export` command followed by the variable name and value.

For example, to create an environment variable called ‘LG_IP’ with a value of ‘192.168.1.10’:

```bash
export LG_IP=192.168.1.10
```

This new environment variable will only exist for the current session. To make an environment variable permanent, you must place it in your user’s .bashrc file:

```bash
nano ~/.bashrc
```

After you place the new `export` line in your `.bashrc` file, use the command below to apply all changes to your current shell session.

```bash
source ~/.bashrc
```

If any of the required environment variables are incorrect or missing, you may experience issues such as silent failures, improper display, or unexpected failures when executing commands. Therefore, checking and verifying environment variable settings is one of the first steps to troubleshooting your Liquid Galaxy configuration.

When an administrator has correctly defined and set environment variables, Liquid Galaxy will have always exhibited consistent behaviour across all master/slave nodes, and a stable working environment will be created and maintained.
