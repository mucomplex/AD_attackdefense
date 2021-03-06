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
Find-UserField -SearchField Description -SearchTerm "built" <br>
#### Get a list of computers in the current domain <br>
Get-NetComputer<br>
Get-NetComputer -OperatingSystem "\*Server 2016\*"<br>
Get-NetComputer -Ping<br>
Get-NetComputer -FullData<br>
#### Get all the groups in the current domain <br>
Get-NetGroup <br>
Get-NetGroup -Domain Hydra.local<br>
Get-NetGroup -FullData <br>
#### Get all groups containing the word "admin" in group name <br>
Get-NetGroup \*admin\* <br>
#### Get all the member of the Domain Admins Group <br>
Get-NetGroupMember -GroupName "Domain Admins" -Recurse <br>
#### Get Group member of user <br>
Get-NetGroup -UserName "mucomplex" <br>
#### List all the localgroup on a machine (need administrator privs on non-dc machines) <br>
Get-NetLocalGroup -ComputerName Hydra.local -ListGroups <br>
#### Get members of all the localgroups on machine (need administrator privs on non-dc machines) <br>
Get-NetLocalGroup -ComputerName Hydra.local -Recurse <br> 
#### Get actively logged users on a computer (need local admin rights on the target) <br>
Get-NetLoggedon -ComputerName Hydra.local <br>
#### Get locally logged users on a computer (need remote registry on the target) <br>
Get-LoggedonLocal -ComputerName Hydra.local <br>
#### Get the last logged user on a computer (need administrator rights and remote registry on targets) <br>
Get-LastLoggedOn -ComputerName Hydra.local <br>
#### Find Shares on hosts in current domain <br>
Invoke-ShareFinder -Verbose <br>
#### Find sensitive files on computers in the domain <br>
Invoke-FileFinder -Verbose <br>
#### Get all fileservers of the domain <br>
Get-NetFileServer <br>
#### list of GPO in current domain <br>
Get-NetGPO <br>
Get-NetGPO -ComputerName HYDRA.local <br>
#### Get GPO use Restricted Group or Group.xml <br>
Get-NetGPOGroup <br>
#### Get users which are in a local group of a machine using GPO <br>
Find-GPOComputerAdmin -Computername HYDRA.local <br>
#### Get machines where the given user is member of specific group <br>
Find-GPOLocation -UserName mucomplex -Verbose <br>
#### Get OUs in a domain <br>
Get-NetOU -FullData <br>
#### Get GPO applied on an OU <br>
Get-NetGPO -GPOname "{gid}" <br>
#### Get the ACLs associated with the specified object <br>
Get-ObjectAcl -SamAccountName mucomplex -ResolveGUIDs <br>
#### Get ACLs associated with the specified prefix <br>
Get-ObjectAcl -ADSprefix 'CN=Administrator,CN=Users' -Verbose <br>
#### Get ACLs associated with specified LDAP path <br>
Get-ObjectAcl -ADSpath "LDAP://CN=Domain Admins,DC=HYDRA,DC=local" -ResolveGUIDs -Verbose <br>
#### Search for interesting ACE <br>
Invoke-ACLScanner -ResolveGUIDs <br>
#### Get ACLs associate with specific path <br>
Get-PathAcl -Path "\\hydra.local\sysvol" <br>
#### Get a list of all domain trust for the current domain<br>
Get-NetDomainTrust<br>
Get-NetDomainTrust -Domain hydra.local<br>
#### Get detail about the current forest <br>
Get-NetForest<br>
Get-NetForest -Forest Hydra.local<br>
#### Get all domains in the current forest<br>
Get-NetForestDomain <br>
Get-NetForestDOmain -Forest hydra.local <br>
#### Forest mapping<br>
Get-NetForestCatalog<br>
Get-NetForestCatalog -Forest hydra.local <br>
#### Map Trust of a forest <br>
Get-NetForestTrust<br>
Get-NetForestTrust -Forest hydra.local<br>
#### Find machine has local admin access <br>
Find-LocalAdminAccess -Verbose<br>
####<br>
Find-WMILocalAdminAcess.ps1 <br>
#### Find local admins on all machines of the domain <br>
Invoke-EnumerateLocalAdmin -Verbose <br>
#### Find Computers where a domain admin has sessions: <br>
Invoke-UserHunter <br>
Invoke-UserHunter -GroupName "RDPUsers" <br>
#### To confirm admin access <br>
Invoke-UserHunter -CheckAccess <br>
#### Find computers where a domain admin is logged-in <br>
Invoke-UserHunter -Stealth <br>
#### Defense <br>
.\NetCease.ps1 <br>


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
#### Get a list of computers in the current domain <br>
Get-ADComputer -Filter * | select Name <br>
Get-ADComputer -Filter 'OperatingSystem -like "\*Server 2016\*" -Properties OperatingSystem | select Name,OperatingSystem <br>
Get-ADComputer -Filter * -Properties *<br>
#### Get all the groups in the current domain <br>
Get-ADGroup -Filter * | select Name <br>
Get-ADGroup -Filter * -Properties * <br>
#### Get all groups containing the word "admin" in group name <br>
Get-ADGroup -Filter 'Name -like "\*admin\*"' | select Name <br>
#### Get all the member of the Domain Admins Group <br>
Get-ADGroupMember -Identity "Domain Admins" -Recursive <br>
#### Get Group member of user <br>
Get-ADPrincipalGroupMembership -Identity mucomplex <br>
#### list of GPO in current domain <br>
Get-GPO -All <br>
Get-GPResutantSetOfPolicy -ReportType Html -Path C:\report.html <br>
#### Get OUs in a domain <br>
Get-ADOrganizationalUnit -Filter * -Properties * <br>
#### Get GPO applied on an OU <br>
Get-GPO -Guid {gid} <br>
#### enumerate ACL without resolve uid <br>
(Get-Acl 'AD:\CN=Administrator,CN=Users,DC=HYDRA,DC=local').Access <br>
#### Get a list of all domain trust for the current domain<br>
Get-ADTrust <br>
Get-ADTrust -Identity hydra.local<br>
#### Get detail about the current forest <br>
Get-ADForest <br>
Get-ADForest -Identity hydra.local <br>
#### Get all domains in the current forest<br>
(Get-ADForest).Domains <br>
#### Forest mapping<br>
Get-ADForest | select -ExpandProperty GlobalCatalogs<br>
#### Map Trust of a forest <br>
Get-ADTrust -Filter 'msDS-TrustFOrestTrustInfo -ne "$null"'<br>

