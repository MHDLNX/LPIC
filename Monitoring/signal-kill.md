In Linux and Unix-like operating systems, signals are a form of inter-process communication used to notify processes of various events. Signals can be sent from one process to another or from the operating system to a process. They are used to handle asynchronous events, like terminating a process or telling it to perform a specific task.

### Common Signals

Here are some of the most commonly used signals:

- **SIGINT (2):** Interrupt signal. Typically sent when the user presses `Ctrl+C`. It requests the process to terminate.
- **SIGTERM (15):** Termination signal. It requests the process to gracefully terminate. The process can handle this signal to perform cleanup before exiting.
- **SIGKILL (9):** Kill signal. It forcefully terminates the process immediately. The process cannot catch or ignore this signal.
- **SIGHUP (1):** Hangup signal. It is sent to a process when the terminal it is associated with is closed. It is often used to tell a daemon to reload its configuration.
- **SIGQUIT (3):** Quit signal. Similar to `SIGINT`, but also produces a core dump, useful for debugging.
- **SIGSTOP (19):** Stop signal. It pauses the process, which can later be resumed with `SIGCONT`.
- **SIGCONT (18):** Continue signal. It resumes a paused process.

### Sending Signals

The `kill` command is commonly used to send signals to processes. Despite its name, `kill` can send any signal, not just termination signals.

#### Basic Usage of `kill`

1. **Send a Signal to a Process:**
   - Syntax: `kill -SIGNAL PID`
   - Example: `kill -SIGTERM 1234`
     - Sends `SIGTERM` to the process with PID 1234.

2. **Send a Termination Signal:**
   - `kill PID`
   - `kill -15 PID`
     - By default, `kill` sends `SIGTERM` (signal 15).

3. **Forcefully Kill a Process:**
   - `kill -9 PID`
     - Sends `SIGKILL` to forcefully terminate the process.

4. **List All Signals:**
   - `kill -l`
     - Displays a list of all available signals.

#### Example Scenarios

1. **Gracefully Terminate a Process:**
   ```bash
   kill -SIGTERM 1234
   ```
   - Sends `SIGTERM` to the process with PID 1234, requesting it to terminate gracefully.

2. **Forcefully Kill a Process:**
   ```bash
   kill -SIGKILL 1234
   ```
   - Sends `SIGKILL` to the process with PID 1234, forcefully terminating it immediately.

3. **Interrupt a Process:**
   ```bash
   kill -SIGINT 1234
   ```
   - Sends `SIGINT` to the process with PID 1234, typically used to interrupt the process (like pressing `Ctrl+C`).

4. **Reload a Daemon Configuration:**
   ```bash
   kill -SIGHUP 1234
   ```
   - Sends `SIGHUP` to the process with PID 1234, often used to reload the configuration of a daemon.

### Handling Signals in Programs

Programs can handle signals by defining signal handlers. A signal handler is a function that gets executed when the process receives a specific signal.

#### Example in C

Here is a simple example of a signal handler in a C program:

```c
#include <stdio.h>
#include <stdlib.h>
#include <signal.h>
#include <unistd.h>

// Signal handler function
void handle_sigint(int sig) {
    printf("Caught signal %d\n", sig);
    exit(1);
}

int main() {
    // Register signal handler for SIGINT
    signal(SIGINT, handle_sigint);

    // Infinite loop to keep the program running
    while (1) {
        printf("Running...\n");
        sleep(1);
    }

    return 0;
}
```

- This program runs an infinite loop, printing "Running..." every second.
- When it receives `SIGINT` (e.g., by pressing `Ctrl+C`), it catches the signal using the `handle_sigint` function and exits.

### Summary

- **Signals** are a mechanism for inter-process communication in Linux, used to notify processes of various events.
- **Common signals** include `SIGINT`, `SIGTERM`, `SIGKILL`, `SIGHUP`, `SIGQUIT`, `SIGSTOP`, and `SIGCONT`.
- The `kill` command is used to send signals to processes.
- **Signal handlers** in programs allow custom handling of specific signals, enabling graceful termination, cleanup, and other custom behaviors.

Understanding signals and how to manage them is crucial for system administration, scripting, and developing robust applications in Unix-like systems.
