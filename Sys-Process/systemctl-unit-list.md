The `systemctl list-units` command in Linux is used to display information about systemd units. Systemd is the system and service manager for many modern Linux distributions, and units are its primary objects for management. Units can be services, sockets, devices, mounts, timers, etc.

### Basic Usage:

```bash
systemctl list-units
```

This command lists all active units. By default, it shows units that are active (loaded and running) and might include various types of units such as services, sockets, targets, etc.

### Common Options:

1. **`--type=`**: Filter the list by unit type. Common types include `service`, `socket`, `device`, `mount`, `automount`, `swap`, `target`, `path`, `timer`, and `slice`.
   ```bash
   systemctl list-units --type=service
   ```

2. **`--all`**: Show all units, including inactive ones.
   ```bash
   systemctl list-units --all
   ```

3. **`--state=`**: Filter the list by unit state, such as `loaded`, `active`, `inactive`, `failed`, etc.
   ```bash
   systemctl list-units --state=failed
   ```

4. **`--failed`**: Show only failed units.
   ```bash
   systemctl list-units --failed
   ```

5. **`--no-pager`**: Disable the pager for long output.
   ```bash
   systemctl list-units --no-pager
   ```

6. **`--quiet`**: Suppress unnecessary output.
   ```bash
   systemctl list-units --quiet
   ```

7. **`--reverse`**: Show the list in reverse order.
   ```bash
   systemctl list-units --reverse
   ```

### Example Usages:

1. **List all active services:**
   ```bash
   systemctl list-units --type=service
   ```

2. **List all units (including inactive):**
   ```bash
   systemctl list-units --all
   ```

3. **List all failed units:**
   ```bash
   systemctl list-units --failed
   ```

4. **List all active and inactive services:**
   ```bash
   systemctl list-units --type=service --all
   ```

5. **List all loaded units (not limited to active):**
   ```bash
   systemctl list-units --state=loaded
   ```

### Understanding the Output:

The output of `systemctl list-units` typically includes the following columns:

- **UNIT**: The name of the unit.
- **LOAD**: Whether the unit's configuration has been loaded.
- **ACTIVE**: The high-level unit activation state (e.g., active, inactive).
- **SUB**: The low-level unit activation state (e.g., running, exited).
- **DESCRIPTION**: A short description of the unit.

### Example Output:

```plaintext
UNIT                               LOAD   ACTIVE SUB     DESCRIPTION
proc-sys-fs-binfmt_misc.automount  loaded active waiting Arbitrary Executable File Formats File System Automount Point
sys-devices-virtual-block-loop0.device loaded active plugged /sys/devices/virtual/block/loop0
systemd-journald.service           loaded active running Journal Service
systemd-logind.service             loaded active running Login Service
```

### Practical Uses:

- **Monitoring Services**: Quickly check which services are running, stopped, or failed.
- **Debugging**: Identify failed services and gather information for troubleshooting.
- **System Administration**: Manage systemd units efficiently, especially in scripts or automated processes.

By using `systemctl list-units` and its various options, you can effectively manage and monitor the state of your system's services and other units.
