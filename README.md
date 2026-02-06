# MultiServer Connectivity Check

This repository provides scripts for verifying basic network connectivity to multiple servers.  
The checks are read‑only and do not modify or authenticate to any remote systems.

## Overview

The scripts perform:

*   ICMP echo requests (ping) to confirm basic network reachability.
*   TCP connection attempts to specified ports using .NET `TcpClient`.
*   Per‑server status output.
*   A final summary listing each server and its resulting status.

These checks are suitable for confirming if servers are online and responding at the network level.

## Features

*   Works across multiple servers in a single execution.
*   Uses .NET networking classes to avoid dependencies on external utilities.
*   Non‑destructive execution with no changes to remote systems.
*   Configurable server list and port list.
*   Produces clear console output and a summary.

## Files

### `Check-Servers.ps1`

A PowerShell script that performs connectivity checks using ICMP and TCP tests.  
Outputs detailed results per server and a final summary in the format:

    <server> - WORKING
    <server> - REACHABLE_NO_PING
    <server> - NOT WORKING

### `Run-Check-Servers.bat`

A batch file that launches the PowerShell script with execution policy bypass for convenience.

## Configuration

Edit the following variables inside `Check-Servers.ps1` to match your environment:

```powershell
$Servers = @(
    'server1',
    'server2'
)

$Ports = @(3389, 445, 80)
```

Only hostnames or IP addresses should be listed.  
Ports may be expanded or replaced depending on the services you need to verify.

## Execution

### Using the batch launcher

Double‑click:

    Run-Check-Servers.bat

This executes the script with an isolated execution policy override.

### Running directly in PowerShell

```powershell
.\Check-Servers.ps1
```

If execution is blocked, adjust policy:

```powershell
powershell -ExecutionPolicy Bypass -File .\Check-Servers.ps1
```

This does not make permanent changes to the system policy.

## Requirements

*   Windows with PowerShell 5 or later.
*   .NET Framework classes available (included by default on Windows systems).
*   Basic network permissions to reach the target servers and ports.

## Notes

*   All tests are unauthenticated and do not access remote system resources.
*   ICMP responses may be blocked on some networks; port results help distinguish this condition.
*   Output should not include production hostnames or internal IP ranges if the repository is public.
