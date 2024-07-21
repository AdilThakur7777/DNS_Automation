# Set global variables for DNS Zone Name and Computer Name

$global:ZoneName = "Zone Name"

$global:ComputerName = "Computer Name"

 

function AddDnsRecord {

    param (

        [string]$recordName,

        [string]$target,

        [string]$recordType

    )

 

    try {

        # Check if the record name already exists for the specified record type

        $existingRecord = Get-DnsServerResourceRecord -ZoneName $global:ZoneName -RRType $recordType.ToUpper() -ComputerName $global:ComputerName -Name $recordName -ErrorAction SilentlyContinue

        

        # If record name already exists for the specified type, output error message and return

        if ($existingRecord) {

            Write-Output "DNS Record with name '$recordName' already exists for $recordType in zone $($global:ZoneName)."

            return

        }

 

        # Validate and check for duplicate target based on record type

        switch ($recordType.ToUpper()) {

            "A" {

                if ($target -match "^\d{1,3}(\.\d{1,3}){3}$") {

                    # Validate IPv4 address format

                    if ($target -notmatch "^(25[0-5]|2[0-4]\d|1\d\d|\d\d?)\.(25[0-5]|2[0-4]\d|1\d\d|\d\d?)\.(25[0-5]|2[0-4]\d|1\d\d|\d\d?)\.(25[0-5]|2[0-4]\d|1\d\d|\d\d?)$") {

                        Write-Output "Invalid IPv4 address '$target'."

                        return

                    }

                    # Check for duplicate IPv4 address

                    $existingTarget = Get-DnsServerResourceRecord -ZoneName $global:ZoneName -RRType "A" -ComputerName $global:ComputerName | Where-Object { $_.RecordData.IPv4Address -eq $target }

                    if ($existingTarget) {

                        Write-Output "IPv4 address '$target' already exists in the DNS zone."

                        return

                    } else {

                       # Add-DnsServerResourceRecordA -Name $recordName -ZoneName $global:ZoneName -IPv4Address $target -ComputerName $global:ComputerName -PassThru

                        Add-DnsServerResourceRecordA -Name $recordName -ZoneName $global:ZoneName -IPv4Address $target -ComputerName $global:ComputerName -PassThru

                        Write-Output "IPv4 DNS Record added successfully."

                    }

                } else {

                    Write-Output "Invalid IPv4 address format '$target'."

                    return

                }

            }

            "AAAA" {

                # Validate IPv6 address format

                if ($target -match "^(?:[0-9a-fA-F]{1,4}:){7}[0-9a-fA-F]{1,4}$") {

                    # Check for duplicate IPv6 address

                    $existingTarget = Get-DnsServerResourceRecord -ZoneName $global:ZoneName -RRType "AAAA" -ComputerName $global:ComputerName | Where-Object { $_.RecordData.IPv6Address -eq $target }

                    if ($existingTarget) {

                        Write-Output "IPv6 address '$target' already exists in the DNS zone."

                        return

                    } else {

                        Add-DnsServerResourceRecordAAAA -Name $recordName -ZoneName $global:ZoneName -IPv6Address $target -ComputerName $global:ComputerName -PassThru

                        Write-Output "IPv6 DNS Record added successfully."

                    }

                } else {

                    Write-Output "Invalid IPv6 address format '$target'."

                    return

                }

            }

            "CNAME" {

                # Validate CNAME target format

                if ($target -match "^[a-zA-Z0-9\-\.]+$") {

                    # Check for duplicate CNAME target

                    $existingTarget = Get-DnsServerResourceRecord -ZoneName $global:ZoneName -RRType "CNAME" -ComputerName $global:ComputerName | Where-Object { $_.RecordData.HostNameAlias -eq $target }

                    if ($existingTarget) {

                        Write-Output "CNAME target '$target' already exists in the DNS zone."

                        return

                    } else {

                        Add-DnsServerResourceRecordCName -Name $recordName -ZoneName $global:ZoneName -HostNameAlias $target -ComputerName $global:ComputerName -PassThru

                        Write-Output "CNAME DNS Record added successfully."

                    }

                } else {

                    Write-Output "Invalid CNAME target '$target'. Only alphanumeric characters, hyphens, and periods are allowed."

                    return

                }

            }

            default {

                Write-Output "Unsupported record type '$recordType'."

                return

            }

        }

    }

    catch {

        Write-Output "Failed to add DNS Record: $recordName"

    }

}

 

function ModifyDnsRecord {

    param (

        [string]$recordName,

        [string]$newIpAddress,

        [string]$recordType

    )

 

    try {

        # Check if the record exists

        $oldObj = Get-DnsServerResourceRecord -ZoneName $global:ZoneName -RRType $recordType.ToUpper() -ComputerName $global:ComputerName -Name $recordName

 

        if ($oldObj) {

            # Record exists, proceed with modification based on the type

            $newObj = $oldObj.Clone()

 

            if ($recordType.ToUpper() -eq "A") {

                # Validate IPv4 address format

                if ($newIpAddress -notmatch "^(25[0-5]|2[0-4]\d|1\d\d|\d\d?)\.(25[0-5]|2[0-4]\d|1\d\d|\d\d?)\.(25[0-5]|2[0-4]\d|1\d\d|\d\d?)\.(25[0-5]|2[0-4]\d|1\d\d|\d\d?)$") {

                    Write-Output "Invalid IPv4 address '$newIpAddress'."

                    return

                }

                $oldIp = $oldObj.RecordData.IPv4Address

                $newObj.RecordData.IPv4Address = $newIpAddress

            }

            elseif ($recordType.ToUpper() -eq "AAAA") {

                # Validate IPv6 address format

                if ($newIpAddress -notmatch "^(?:[0-9a-fA-F]{1,4}:){7}[0-9a-fA-F]{1,4}$") {

                    Write-Output "Invalid IPv6 address format '$newIpAddress'."

                    return

                }

                $oldIp = $oldObj.RecordData.IPv6Address

                $newObj.RecordData.IPv6Address = $newIpAddress

            }

            elseif ($recordType.ToUpper() -eq "CNAME") {

                # Validate CNAME target format

                if ($newIpAddress -notmatch "^[a-zA-Z0-9\-\.]+$") {

                    Write-Output "Invalid CNAME target '$newIpAddress'. Only alphanumeric characters, hyphens, and periods are allowed."

                    return

                }

                $oldIp = $oldObj.RecordData.HostNameAlias

                $newObj.RecordData.HostNameAlias = $newIpAddress

            }

 

            Set-DnsServerResourceRecord -ZoneName $global:ZoneName -OldInputObject $oldObj -NewInputObject $newObj -ComputerName $global:ComputerName -PassThru

            

            # Prepare output message

            $output = @"

Old $recordType Address: $oldIp

New $recordType Address: $newIpAddress

"@

            

            Write-Output $output

        } else {

            # Record does not exist

            Write-Output "No Record Found for name : $recordName"

        }

    }

    catch {

        Write-Output "Failed to modify DNS Record: $recordName"

    }

}

 

function DeleteDnsRecord {

    param (

        [string]$recordName,

        [string]$recordType

    )

 

    try {

        # Check if the record exists

        $existingRecord = Get-DnsServerResourceRecord -ZoneName $global:ZoneName -RRType $recordType.ToUpper() -ComputerName $global:ComputerName -Name $recordName

 

        if ($existingRecord) {

            # Proceed with deletion based on the type

            Remove-DnsServerResourceRecord -ZoneName $global:ZoneName -Name $recordName -RRType $recordType.ToUpper() -ComputerName $global:ComputerName -Force

            Write-Output "$recordType DNS Record '$recordName' has been deleted."

        } else {

            # Record does not exist

            Write-Output "No $recordType Record Found for name : $recordName in zone $($global:ZoneName)."

        }

    }

    catch {

        Write-Output "Failed to delete DNS Record: $recordName"

    }

}

 

function ProcessCsv {

    param (

        [string]$csvFilePath

    )

 

    # Import the CSV file

    $csvData = Import-Csv -Path $csvFilePath

 

    # Iterate through each row in the CSV

    foreach ($row in $csvData) {

        $operation = $row.Operation

        $recordName = $row.RecordName

        $target = $row.Target

        $newTarget = $row.NewTarget

        $recordType = $row.RecordType

 

        switch ($operation.ToLower()) {

            "add" {

                AddDnsRecord -recordName $recordName -target $target -recordType $recordType

            }

            "modify" {

                ModifyDnsRecord -recordName $recordName -newIpAddress $newTarget -recordType $recordType

            }

            "delete" {

                DeleteDnsRecord -recordName $recordName -recordType $recordType

            }

            default {

                Write-Output "Unsupported operation '$operation' in CSV file."

            }

        }

    }

}

 

# Define the path to the CSV file

$csvFilePath = "C:\Users\adil.thakur.adm\Downloads\2nd.csv"

 

# Process the CSV file

ProcessCsv -csvFilePath $csvFilePath
