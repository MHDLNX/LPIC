Sure, let's dive deeper into `systemctl` commands and options, with more examples to illustrate its usage.

### More Examples with `systemctl`

#### Basic Service Management

1. **Start a Service:**
   ```bash
   sudo systemctl start nginx.service
   ```
   This command starts the `nginx` service.

2. **Stop a Service:**
   ```bash
   sudo systemctl stop nginx.service
   ```
   This command stops the `nginx` service.

3. **Restart a Service:**
   ```bash
   sudo systemctl restart nginx.service
   ```
   This command restarts the `nginx` service.

4. **Reload a Service:**
   ```bash
   sudo systemctl reload nginx.service
   ```
   This command reloads the `nginx` service configuration without stopping it.

5. **Enable a Service:**
   ```bash
   sudo systemctl enable nginx.service
   ```
   This command enables the `nginx` service to start on boot.

6. **Disable a Service:**
   ```bash
   sudo systemctl disable nginx.service
   ```
   This command disables the `nginx` service from starting on boot.

7. **Check the Status of a Service:**
   ```bash
   systemctl status nginx.service
   ```
   This command shows the current status of the `nginx` service, including whether it's running, any recent log entries, and its PID.

#### Advanced Service Management

1. **Mask a Service:**
   ```bash
   sudo systemctl mask nginx.service
   ```
   This command prevents the `nginx` service from being started manually or automatically.

2. **Unmask a Service:**
   ```bash
   sudo systemctl unmask nginx.service
   ```
   This command unmasks the `nginx` service, allowing it to be started again.

3. **Reload `systemd` Configuration:**
   ```bash
   sudo systemctl daemon-reload
   ```
   This command reloads the `systemd` manager configuration. Use this after modifying unit files.

4. **Show All Units:**
   ```bash
   systemctl list-units
   ```
   This command lists all units currently loaded, whether active or inactive.

5. **List All Unit Files:**
   ```bash
   systemctl list-unit-files
   ```
   This command lists all unit files installed on the system, along with their enablement status.

6. **Check Failed Units:**
   ```bash
   systemctl --failed
   ```
   This command lists units that have failed to start.

#### System State Management

1. **Reboot the System:**
   ```bash
   sudo systemctl reboot
   ```
   This command reboots the system.

2. **Power Off the System:**
   ```bash
   sudo systemctl poweroff
   ```
   This command shuts down and powers off the system.

3. **Suspend the System:**
   ```bash
   sudo systemctl suspend
   ```
   This command suspends the system (puts it into a low-power state).

4. **Hibernate the System:**
   ```bash
   sudo systemctl hibernate
   ```
   This command hibernates the system (saves the current state to disk and powers off).

5. **Hybrid Sleep:**
   ```bash
   sudo systemctl hybrid-sleep
   ```
   This command suspends the system to both RAM and disk (a combination of suspend and hibernate).

#### Viewing Logs

1. **View Logs for a Specific Unit:**
   ```bash
   journalctl -u nginx.service
   ```
   This command shows log entries for the `nginx` service.

2. **View Logs Since the Last Boot:**
   ```bash
   journalctl -b
   ```
   This command shows all log entries since the last system boot.

3. **Follow Live Logs:**
   ```bash
   journalctl -f
   ```
   This command shows live log entries as they are added.

### Detailed `systemctl` Options

- **`start`**: Start a service.
- **`stop`**: Stop a service.
- **`restart`**: Restart a service.
- **`reload`**: Reload a service’s configuration.
- **`enable`**: Enable a service to start at boot.
- **`disable`**: Disable a service from starting at boot.
- **`status`**: Show the status of a service.
- **`is-active`**: Check if a service is active.
- **`is-enabled`**: Check if a service is enabled.
- **`mask`**: Completely disable a service.
- **`unmask`**: Re-enable a masked service.
- **`daemon-reload`**: Reload `systemd` manager configuration.
- **`list-units`**: List loaded units.
- **`list-unit-files`**: List all installed unit files.
- **`--failed`**: Show failed units.
- **`reboot`**: Reboot the system.
- **`poweroff`**: Power off the system.
- **`suspend`**: Suspend the system.
- **`hibernate`**: Hibernate the system.
- **`hybrid-sleep`**: Hybrid sleep (suspend to both RAM and disk).

### Example Workflow

Let's say you want to manage the Apache web server (`apache2`):

1. **Install Apache:**
   ```bash
   sudo apt update
   sudo apt install apache2
   ```

2. **Start Apache:**
   ```bash
   sudo systemctl start apache2.service
   ```

3. **Enable Apache to Start on Boot:**
   ```bash
   sudo systemctl enable apache2.service
   ```

4. **Check Apache Status:**
   ```bash
   systemctl status apache2.service
   ```

5. **View Apache Logs:**
   ```bash
   journalctl -u apache2.service
   ```

6. **Restart Apache:**
   ```bash
   sudo systemctl restart apache2.service
   ```

7. **Stop Apache:**
   ```bash
   sudo systemctl stop apache2.service
   ```

8. **Disable Apache from Starting on Boot:**
   ```bash
   sudo systemctl disable apache2.service
   ```

### Summary

`systemd` and `systemctl` provide a powerful and flexible way to manage system services and states on modern Linux systems. Understanding these tools allows you to control service behavior, manage dependencies, and ensure your system operates smoothly and efficiently.
