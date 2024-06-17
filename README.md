# BgInfo-Setup

## PowerShell script to get TeamViewer ID


Save the following as 'GetTeamViewerID.ps1'
```powershell
$paths = @(
    "HKLM:\SOFTWARE\WOW6432Node\TeamViewer",
    "HKLM:\SOFTWARE\TeamViewer",
    "HKLM:\SOFTWARE\WOW6432Node\TeamViewer GmbH\TeamViewer",
    "HKLM:\SOFTWARE\TeamViewer GmbH\TeamViewer"
)

foreach ($path in $paths) {
    if (Test-Path $path) {
        $teamViewerID = Get-ItemProperty -Path $path -Name "ClientID" -ErrorAction SilentlyContinue | Select-Object -ExpandProperty ClientID
        if ($teamViewerID) {
            Write-Output "TeamViewer ID: $teamViewerID"
            break
        }
    }
}

if (-not $teamViewerID) {
    Write-Output "TeamViewer ID not found in the expected registry paths."
}

```

