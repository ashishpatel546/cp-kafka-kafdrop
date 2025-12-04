# Windows PowerShell Setup - Complete

## Profile Location

Your PowerShell profile has been created at:

```
C:\Users\AshishKumar3\OneDrive - WPP Cloud\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1
```

## Available Aliases and Functions

### 1. **grep** - Text Search

Alias for `Select-String` to work like grep on Mac/Linux.

```powershell
# Example usage:
Get-Content file.txt | grep "search-term"
ls | grep "pattern"
```

### 2. **cp-kafka-start** - Start Kafka Server

Starts the Kafka server using Docker Compose from this repository.

```powershell
cp-kafka-start
```

After starting, access:

- Kafdrop UI: http://localhost:9000
- Control Center: http://localhost:9021

### 3. **cp-kafka-stop** - Stop Kafka Server

Stops the Kafka server and all related services.

```powershell
cp-kafka-stop
```

### 4. **redis-server** - Start Redis Server

Starts a Redis server in Docker on port 6379.

```powershell
redis-server
```

### 5. **redis-cli** - Access Redis CLI

Opens an interactive Redis CLI session.

```powershell
redis-cli
```

### 6. **refresh** - Reload Profile

Reloads the PowerShell profile to make newly added aliases available without restarting the terminal.

```powershell
refresh
```

## Profile Compatibility

The profile works across:

- ✅ VS Code integrated terminal
- ✅ Windows PowerShell terminal
- ✅ Windows Terminal (PowerShell)
- ✅ Any PowerShell 5.1 session

## How to Add New Aliases

1. Open the profile file:

   ```powershell
   notepad $PROFILE
   ```

2. Add your new alias or function

3. Save the file

4. Run `refresh` in your terminal to load the changes immediately

## Notes

- All aliases are loaded automatically when you open a new PowerShell terminal
- The profile displays a welcome message showing all available custom aliases
- Docker must be running for Kafka and Redis commands to work
