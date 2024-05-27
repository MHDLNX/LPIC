In a Linux shell, the username and hostname are important pieces of information that help identify the user and the machine they are logged into. This information is often displayed in the command prompt and can be useful for scripting and system administration tasks.

### Viewing Username and Hostname in the Shell

1. **Username:**
   - The `whoami` command prints the current logged-in user's username.
     ```bash
     whoami
     ```
   - The `id` command also provides the username along with user ID and group information.
     ```bash
     id -un
     ```

2. **Hostname:**
   - The `hostname` command prints the system's hostname.
     ```bash
     hostname
     ```
   - The `uname -n` command also provides the hostname.
     ```bash
     uname -n
     ```

### Command Prompt Customization

The shell prompt (PS1) often includes the username and hostname to provide context about the current session. This can be customized by modifying the `PS1` variable in your shell configuration file (like `.bashrc` or `.bash_profile` for Bash).

#### Example Prompt Customization

In Bash, the default prompt might look like this:
```bash
[user@hostname directory]$
```

You can customize the prompt by editing the `.bashrc` file in your home directory:
```bash
nano ~/.bashrc
```

Add or modify the `PS1` variable to include the username (`\u`), hostname (`\h`), and current working directory (`\w`):
```bash
PS1='\u@\h:\w\$ '
```

After editing, apply the changes by sourcing the `.bashrc` file:
```bash
source ~/.bashrc
```

### Using Username and Hostname in Scripts

Sometimes, you may need to use the username and hostname within a shell script.

#### Example Script

Here is a simple script that prints the username and hostname:
```bash
#!/bin/bash

# Get the username
USER_NAME=$(whoami)

# Get the hostname
HOST_NAME=$(hostname)

# Print the username and hostname
echo "Username: $USER_NAME"
echo "Hostname: $HOST_NAME"
```

Save this script to a file, for example, `userinfo.sh`, and make it executable:
```bash
chmod +x userinfo.sh
```

Run the script:
```bash
./userinfo.sh
```

### Summary

- **Viewing Username:** Use the `whoami` or `id -un` command.
- **Viewing Hostname:** Use the `hostname` or `uname -n` command.
- **Customizing Prompt:** Modify the `PS1` variable in your shell configuration file to include `\u` (username) and `\h` (hostname).
- **Scripting:** Use `whoami` and `hostname` commands within scripts to obtain and use the username and hostname.

These commands and techniques help you manage and personalize your Linux environment effectively.
