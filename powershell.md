#

## AD expired passwords

```
Get-ADUser -filter {Enabled -eq $True -and PasswordNeverExpires -eq $False} –Properties "samaccountname", "msDS-UserPasswordExpiryTimeComputed" | Select-Object -Property "samaccountname",@{Name="ExpiryDate";Expression={[datetime]::FromFileTime($_."msDS-UserPasswordExpiryTimeComputed")}} | sort ExpiryDate
```

## AD User

```
get-aduser -searchbase "OU=User,DC=test,DC=domain" -Properties created -Filter * |?{$_.created -gt $(Get-Date).AddDays(-230)} | select Name,Created|Sort-Object created
```

## Test windows credentials

```
Function Test-ADAuthentication {
    param($username,$password)
    (new-object directoryservices.directoryentry "",$username,$password).psbase.name -ne $null
    }
```

> PS C:\> Test-ADAuthentication "dom\myusername" "mypassword"
> True

## Change network profile

```
Get-NetConnectionProfile
```

```
Set-NetConnectionProfile -NetworkCategory Private
```
