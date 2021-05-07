## List of prerequisites

### Java Runtime Environment
*https://www.java.com/fr/download/*
<br/><br/>

### Java Class "GetBase64OaepSHA1EncryptedString"
- *Class directory in global variable ``JavaClassPath``*
- *Class name in global variable ``JavaClassName``*
<br/><br/>

### ActiveDirectory Powershell module
```powershell
Install-Module -name ActiveDirectory
```
<br/>

### ExchangeOnlineManagement Powershell module 
- Full path in global variable ``EXOLModulePath``
<br/><br/>

## Base functions

### Set-GlobalVars
*Configure the global variables specific to the environment*
<br/>
More details with Get-Help :
```powershell
Get-Help -detailed Set-GlobalVars
```
<br/>

### Get-AccessToken
*Retrieves a Bearer token, to be passed as a parameter to the function that queries the Rest webservice*
<br/><br/>

### Get-PersonPhotoSyncSummary
*Retrieves a list of profiles changed from a specified number of days (or 7 by default).*
- __Required__ : ``$Token`` (retrieved using ``Get-AccessToken``)
- Result is analyzed, and a custom object is returned with the list of valid profiles: the profiles with the default photo or no photos or without a linked AD Login are rejected.
In case of invalid format, the profile is set aside but kept in the exported object/json.
<br/><br/>

### Sync-ArgosPhotosToAD
*Compares a list of profiles passed to Active Directory thumbnails and do update if needed*
- **Photos that match the size criteria and are different from the attached photos are replaced in AD**
- the photos are retrieved via the webservice, or directly in a directory/share to be specified as a global variable ``PhotoSourcePath``
- The photos must be in Jpeg format, or Png format; in cas of Png format, maximum size can be 10 times higher than the limit (10 * 10 KB by default), because they are compressed in Jpeg format on the fly.
<br/><br/>

### Sync-ArgosPhotosToEXOL
*Compares a list of profiles passed to Exchange Online profile photos*
- **Photos that match the size criteria and are different from the attached photos are replaced in Exchange Online.**