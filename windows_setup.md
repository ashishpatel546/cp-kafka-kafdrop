# Windows PowerShell Profile Setup Requirements

## Objective

Set up PowerShell aliases and functions for Windows that work seamlessly across VS Code terminal, PowerShell terminal, and Windows Terminal. All terminals must use the same `$PROFILE` configuration.

## Prerequisites

- Windows PowerShell 5.1 or later
- Docker Desktop installed and running
- VS Code (for `open-zsh` command)

## Profile Location

Create/update the PowerShell profile at: `$PROFILE` (typically at `C:\Users\<username>\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1`)

## Required Aliases and Functions

### 1. Utility Aliases

- **grep**: Alias for `Select-String` to provide Mac/Linux-like grep functionality

### 2. Kafka Management

- **cp-kafka-start**: Start Kafka server using Docker Compose

  - Path: `d:\Ashish\Repos\cp-kafka-kafdrop\docker-compose.yml`
  - Should start all services (Zookeeper, Kafka, Schema Registry, Control Center, Kafdrop)
  - Display access URLs after startup:
    - Kafdrop UI: http://localhost:9000
    - Control Center: http://localhost:9021

- **cp-kafka-stop**: Stop Kafka server and all related services
  - Uses `docker-compose down` command

### 3. Git Configuration

- **gsetlocal**: Set local Git config

  - User: `Ashish Patel`
  - Email: `ashi.patel546@gmail.com`
  - Uses `git config` (local repository only)

- **gsetglobal**: Set global Git config
  - User: `Ashish Kumar`
  - Email: `ashish.kumar3@vml.com`
  - Uses `git config --global`

### 4. Redis Management

- **redis-server**: Start Redis server in Docker

  - Container name: `redis-local`
  - Port: 6379
  - Image: `redis:latest`
  - Should run in detached mode

- **redis-stop**: Stop Redis server

  - Check if Redis container exists before stopping
  - If container doesn't exist, display error message
  - If exists, stop and remove the `redis-local` container
  - Display confirmation message

- **redis-cli**: Access Redis CLI
  - Check if Redis server is running first
  - If not running, display error message with instructions
  - If running, connect to the `redis-local` container and open interactive Redis CLI session

### 5. Profile Management

- **refresh**: Reload PowerShell profile immediately

  - Should source `$PROFILE` to apply new aliases without restarting terminal
  - Display confirmation message after reload

- **aliases**: Display all available custom aliases and functions

  - Show formatted list of all custom commands
  - Include brief description for each

- **open-zsh**: Open PowerShell profile in VS Code for editing
  - Uses `code $PROFILE` command

## Implementation Details

### Profile Structure

1. Check if `$PROFILE` exists, create if not: `New-Item -Path $PROFILE -ItemType File -Force`
2. Create functions (not simple aliases) for complex commands
3. Use `Set-Alias` for simple command replacements
4. Include colored output using `Write-Host` with `-ForegroundColor`
5. Add a welcome message that displays on profile load

### Function Requirements

- Use absolute paths for Docker Compose file references
- Include user feedback messages (starting, stopping, success, etc.)
- Use appropriate colors:
  - Green: Success messages
  - Yellow: Warning/In-progress messages
  - Cyan: Information (URLs, etc.)
  - White: List items

### Welcome Message

Display on profile load:

- Confirmation that profile loaded successfully
- List of all available custom aliases
- Use consistent formatting

## Testing

After setup, verify:

1. Profile loads without errors: `. $PROFILE`
2. All commands are registered: `Get-Command cp-kafka-start, cp-kafka-stop, gsetlocal, gsetglobal, redis-server, redis-stop, redis-cli, refresh, grep, aliases, open-zsh`
3. `refresh` command works to reload profile
4. `aliases` displays all custom commands
5. `open-zsh` opens profile in VS Code
6. `gsetlocal` sets local Git config correctly
7. `gsetglobal` sets global Git config correctly

## Expected Behavior

- Profile automatically loads when opening any PowerShell terminal
- All aliases work in VS Code terminal, PowerShell terminal, and Windows Terminal
- New aliases become available after running `refresh` without terminal restart
- Commands provide clear feedback about actions being performed
