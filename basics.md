# PowerShell Basics

[Installing Powershell](https://docs.microsoft.com/en-us/powershell/scripting/windows-powershell/install/installing-windows-powershell?view=powershell-7.2.0)

## help system


```powershell
# version PowerShell
$PSVersionTable

# get execution policy
Get-ExecutionPolicy
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned


#get any service
Get-Service -Name W32Time

#get help system
#Get-Command -Noun Process
Get-Command
Help
get-Help 
Get-Help -Name Get-Help
Get-Help -Name Get-Help -Full
help Get-Help -Parameter Name
Get-Help -Name Get-Command -Full
Get-Help -Name Get-Command -Detailed
Get-Help -Name Get-Command -Examples
Get-Help -Name Get-Command -Online
Get-Help -Name Get-Command -Parameter Noun
Get-Help -Name Get-Command -ShowWindow
help *process*
help pr*cess

Get-Member
```

## Objects, properties and methids

```powershell
# get object
Get-Service -Name w32time | Get-Member
Get-Command -ParameterType ServiceController
Get-Service -Name w32time | Select-Object -Property *
Get-Service -Name w32time | Select-Object -Property Status, Name, DisplayName, ServiceType

# get method
Get-Service -Name w32time | Get-Member -MemberType Method
(Get-Service -Name w32time).Stop()
Get-Process -Name PowerShell
Start-Service -Name w32time | Get-Member
Get-Service -Name w32time | Out-Host | Get-Member

#active directory
Get-Command -Module ActiveDirectory
Get-ADUser -Identity mike | Get-Member

```

## Oneliners and pipeline
key things to talk
whatif
export
compare
convert
compare
measure
confirm


```powershell
# oneliners
Get-Service |
  Where-Object CanPauseAndContinue -eq $true |
    Select-Object -Property *

# line separation
$Service = 'w32time'; Get-Service -Name $Service

Get-Service |
Where-Object CanPauseAndContinue |
Select-Object -Property DisplayName, Status

# the pipeline
get-help about_pipelines
'w32time' | Get-Member

$CustomObject = [pscustomobject]@{
 Name = 'w32time'
 }
 $CustomObject | Get-Member

'Background Intelligent Transfer Service', 'Windows Time' | Out-File -FilePath $env:TEMP\services.txt

# powershell get
Find-Module -Name MrToolkit
Find-Module -Name MrToolkit | Install-Module
# find pipeline input with MrToolkit
Get-MrPipelineInput -Name Stop-Service

```

## Formating, aliases, providers, comparisons

```powershell  
# formating
Get-Service -Name w32time | Select-Object -Property Status, DisplayName, Can*
Get-Service -Name w32time | Select-Object -Property Status, DisplayName, Can* | Format-Table
Get-Service -Name w32time | Format-List
Get-Service -Name w32time | Format-List | Get-Member


#aliases
Get-Alias -Name gcm
Get-Alias -Name gcm, gm
Get-Alias gm

#providers
Get-PSProvider
Get-PSDrive

Import-Module -Name ActiveDirectory, SQLServer
Get-PSProvider

Get-ChildItem -Path Cert:\LocalMachine\CA

# Comparison Operators
get-help *comparison*
'PowerShell' -eq 'powershell'
'PowerShell' -ceq 'powershell'
'PowerShell' -match '^*.shell$'

#range operator
$Numbers = 1..10
$Numbers -notcontains 10
15 -in $Numbers

#replace operator
'PowerShell' -replace 'Shell'

```

## Flow control

```powershell
#looping
'ActiveDirectory', 'SQLServer' |
   ForEach-Object {Get-Command -Module $_} |
     Group-Object -Property ModuleName -NoElement |
         Sort-Object -Property Count -Descending

#for
for ($i = 1; $i -lt 5; $i++) {
  Write-Output "Sleeping for $i seconds"
  Start-Sleep -Seconds $i
}

#do
$number = Get-Random -Minimum 1 -Maximum 10
do {
  $guess = Read-Host -Prompt "What's your guess?"
  if ($guess -lt $number) {
    Write-Output 'Too low!'
  }
  elseif ($guess -gt $number) {
    Write-Output 'Too high!'
  }
}
until ($guess -eq $number)

#while
$date = Get-Date -Date 'November 22'
while ($date.DayOfWeek -ne 'Sunday') {
  $date = $date.AddDays(1)
}
Write-Output $date

#break continue and return
for ($i = 1; $i -lt 5; $i++) {
  Write-Output "Sleeping for $i seconds"
  Start-Sleep -Seconds $i
  break
}

while ($i -lt 5) {
  $i += 1
  if ($i -eq 3) {
    continue
  }
  Write-Output $i
}

$number = 1..10
foreach ($n in $number) {
  if ($n -ge 4) {
    Return $n
  }
}
```

## Working with outputs

```powershell
# Console Output (Out-Host)
Get-Command | Out-Host -Paging

# Format-List
Get-Process | Out-Host -Paging | Format-List
Get-Process | Format-List | Out-Host -Paging

# out-null
Get-Command | Out-Null #usefull when checking for errors

# out-printer
Get-Command Get-Command | Out-Printer -Name 'Microsoft Office Document Image Writer'

# out-File
Get-Process | Out-File -FilePath C:\temp\processlist.txt
Get-Process | Out-File -FilePath C:\temp\processlist.txt -Encoding ASCII
Get-Command | Out-File -FilePath c:\temp\output.txt -Width 2147483647 #max line width

# formatting output
Get-Command -Verb Format -Module Microsoft.PowerShell.Utility

# format-wide
Get-Command -Verb Format | Format-Wide
Get-Command -Verb Format | Format-Wide -Property Noun -Column 3
Get-Process  | Format-List -Property ProcessName,FileVersion,StartTime,Id

# using-format table
Get-Service -Name win* | Format-Table
Get-Service -Name win* | Format-Table -AutoSize # no truncated text
Get-Service -Name win* | Format-Table -Property Name,Status,StartType,DisplayName,DependentServices -AutoSize
Get-Service -Name win* | Format-Table -Property Name,Status,StartType,DisplayName,DependentServices -Wrap

# organizing output - groupby
Get-Service -Name win* | Sort-Object StartType | Format-Table -GroupBy StartType

```

## Managing current location and working with files

```powershell
Get-Location
Set-Location -Path C:\Windows
Set-Location -Path .. -PassThru
Set-Location -Path HKLM:\SOFTWARE -PassThru
Set-Location -Path .. -PassThru
#same as
cd -Path C:\Windows
chdir -Path .. -PassThru
sl -Path HKLM:\SOFTWARE -PassThru

# Saving and Recalling Recent Locations (Push-Location and Pop-Location)
Get-Location
Push-Location -Path "Local Settings"
Push-Location -Path Temp
Pop-Location
Get-Location

# listig all files and folders in a folder
Get-ChildItem -Path C:\ -Force
Get-ChildItem -Path C:\ -Force -Recurse
Get-ChildItem -Path $env:ProgramFiles -Recurse -Include *.exe | Where-Object -FilterScript {($_.LastWriteTime -gt '2005-10-01') -and ($_.Length -ge 1mb) -and ($_.Length -le 10mb)}

# copy files and folders
Copy-Item -Path C:\boot.ini -Destination C:\boot.bak
Copy-Item -Path C:\boot.ini -Destination C:\boot.bak -Force
Copy-Item -Filter *.txt -Path c:\data -Recurse -Destination C:\temp\text
(New-Object -ComObject Scripting.FileSystemObject).CopyFile('C:\boot.ini', 'C:\boot.bak')

# creating files and folders
New-Item -Path 'C:\temp\New Folder' -ItemType Directory
New-Item -Path 'C:\temp\New Folder\file.txt' -ItemType File
Remove-Item -Path C:\temp\DeleteMe
Remove-Item -Path C:\temp\DeleteMe -Recurse

#mapping drive
New-PSDrive -Name P -Root $env:ProgramFiles -PSProvider FileSystem

#reading file
Get-Content -Path C:\boot.ini
(Get-Content -Path C:\boot.ini).Length

Get-ChildItem -Path C:\Windows Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Window

```

## New Stuff

```powershell
# The API enables users to discover, edit, and execute full commands based on matching predictions from the user's history.
Set-PSReadLineOption -PredictionSource History
```

## Types

### Arrays

```powershell
# Arrays
$items = 10,"blue",12.54e3,16.30D # 1-D array of length 4
$items[1] = -2.345
$items[2] = "green"

$a = New-Object 'object[,]' 2,2 # 2-D array of length 4
$a[0,0] = 10
$a[0,1] = $false
$a[1,0] = "red"
$a[1,1] = $null

# Constraining element types
$a = [int[]](1,2,3,4)   # constrained to int
$a[1] = "abc"           # implementation-defined behavior
$a += 1.23              # new array is unconstrained

# Arrays as reference types
$a = 10,20                     # $a refers to an array of length 2
$a = 10,20,30                  # $a refers to a different array, of length 3
$a = "red",10.6                # $a refers to a different array, of length 2
$a = New-Object 'int[,]' 2,3   # $a refers to an array of rank 2

$a = 10,20,30
">$a<"
$b = $a         # make $b refer to the same array as $a
">$b<"

$a[0] = 6       # change value of [0] via $a
">$a<"
">$b<"          # change is reflected in $b

$b += 40        # make $b refer to a new array
$a[0] = 8       # change value of [0] via $a
">$a<"
">$b<"          # change is not reflected in $b

# Arrays as array elements
$colors = "red", "blue", "green"
$list = $colors, (,7), (1.2, "yes") # parens in (,7) are redundant; they
                                    # are intended to aid readability
"`$list refers to an array of length $($list.Length)"
">$($list[1][0])<"
">$($list[2][1])<"


#enumerating array
$a = 10, 53, 16, -43
foreach ($elem in $a) {
    # do something with element via $e
}

foreach ($elem in -5..5) {
    # do something with element via $e
}

$a = New-Object 'int[,]' 3, 2
foreach ($elem in $a) {
    # do something with element via $e
}

```

### Hash Tables

```powershell
$h1 = @{ FirstName = "James"; LastName = "Anderson"; IDNum = 123 }
$h1.FirstName # designates the key FirstName
$h1["LastName"] # designates the associated value for key LastName
$h1.Keys # gets the collection of keys

#Adding and removing Hashtable elements
$h1 = @{ FirstName = "James"; LastName = "Anderson"; IDNum = 123 }
$h1.Dept = "Finance" # adds element Finance
$h1["Salaried"] = $false # adds element Salaried
$h1.Remove("Salaried") # removes element Salaried

#Enumerating over a Hashtable
$h1 = @{ FirstName = "James"; LastName = "Anderson"; IDNum = 123}
foreach ($e in $h1.Keys) {
   "Key is " + $e + ", Value is " + $h1[$e]
}
```
