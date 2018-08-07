# IfNeitherAddOne-PowerShell
Simple Powershell script so that if a user is not in either of the groups we're searching add them to one of them.
This was initially setup to add all users who aren't in an MFA group or Non-MFA group added to the Non-MFA group.



```
###Add users not in either group to the first Group###

#Set Variables being used in our sections that determine and set local group membership

$Group1 = Get-ADGroupMember -Identity "CHANGE TO GROUP 1" -Recursive | Select-Object -ExpandProperty SamAccountName
$Group2 = Get-ADGroupMember -Identity "CHANGE TO GROUP 1" -Recursive | Select-Object -ExpandProperty SamAccountName

Get-ADUser -Filter * |
ForEach {
        $_.SamAccountName
        If (-not($Group1 -contains $_.SamAccountName -or $Group2 -contains $_.SamAccountName)){
        Add-ADGroupMember -Identity 'CHANGE TO DESTINATION GROUP' -Members $_.SamAccountName 
    }
}
```
