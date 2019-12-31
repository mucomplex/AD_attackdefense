# Enumeration with .NET
$ADClass = [System.DirectoryServices.ActiveDirectory.Domain]<br>
$ADClass::GetCurrentDomain()<br>
<br>
# PowerView<br>
#### Get Current Domain<br>
Get-NetDomain<br>
#### Get Object of another domain<br>
Get-NetDomain -Domain Hydra.local<br>
#### Get domain SID for current Domain<br>
Get-DomainSID<br>
#### Policy<br>
Get-DomainPolicy<br>
(Get-DomainPolicy)."system access"<br>
#### Get domain controllers for the current domain<br>
Get-NetDomainController<br>
Get-NetDomainCOntroller -Domain moneycorp.local<br>
#### Get a list of users in the current domain<br>
Get-NetUser<br>
Get-NetUser -Username mucomplex<br>
#### Get list of all properties for user in the current domain<br>
Get-UserProperty<br>
Get-UserProperty -Properties pwdlastset<br>
#### Read for Description <br>
Find-UserField -SearchField Description -SearchTerm "built"

# ActiveDirectory PowerShell module<br>
#### Get Current Domain<br>
Get-ADDomain<br>
#### Get object of another domain<br>
Get-ADDomain -Identity Hydra.local<br>
#### Get domain SID for the current domain<br>
(Get-ADDomain).DomainSID<br>
#### Get domain controllers for the current domain<br>
Get-ADDomainController<br>
Get-ADDomainController -DomainName HYDRA.local -Discover<br>
#### Get a list of users in the current domain<br>
Get-ADUser -Filter * -Properties *<br>
Get-ADUser -Identity mucomplex -Properties *<br>
#### Get list of all properties for users in the current domain<br>
Get-ADUser -Filter * -Properties * | Select  -First 1 | Get-Member -MemberType \*Property | Select Name<br>
#### Read for Description <br>
Get-ADUser -Filter '"Description -like "\*built\*"' -Properties Description | Select name,Description <br>



