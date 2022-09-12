# Octopus Deploy asp.net core web api application to local desktop machine

asp.net core web api can be run as server exe under dotnet core framework. so after this project is published, we need to pack it and then deploy it by Octopus deploy server to my laptop

steps:

1, create an asp.web api project in VS 2022.
2, run "dotnet publish webapmicro.csproj  --output webcoreapp --configuration release"
3, run  "octo pack --id webapmicro --version 1.0.0 --basepath webcoreapp", this created webapmicro.1.0.0.nupkg (deploying package) 
4, configure octpous deployment environment called development
5, go to library select package to upload package nupkg file, the UI will show package id webapmicro
6, go to projects menu to Add a new project to start deployment
7, click "process" and search "deploy to IIS" and add this template 
8, use package id to complete process.
9, create a release and click "deploy to..."
10, deploy will be successful 
11, copy tasklog to find out where exe is deployed as below
<table>
<tr>
<td>

5 additional lines not shown
September 12th 2022 20:51:28Info
Set .NET framework version: v4.0 
September 12th 2022 20:51:28Info
Site "OctDeploy" does not exist, creating... 
September 12th 2022 20:51:28Info
Name             ID   State      Physical Path                  Bindings                                                
September 12th 2022 20:51:29Info
----             --   -----      -------------                  --------                                                
September 12th 2022 20:51:29Info
OctDeploy        3    Started    C:\Octopus\Applications\develo http :81:od-temp.example.com                            
September 12th 2022 20:51:29Info
                                 pment\webapmicro\1.0.0_2                                                               
September 12th 2022 20:51:29Info
Assigning "IIS:\Sites\OctDeploy" to application pool "OctDeploy"... 
September 12th 2022 20:51:29Info
Setting physical path of IIS:\Sites\OctDeploy to<b>C:\Octopus\Applications\development\webapmicro\1.0.0_2 </b>
September 12th 2022 20:51:29Info
Comparing existing IIS bindings with configured bindings... 
September 12th 2022 20:51:29Info
Found existing non-configured binding: http :81:od-temp.example.com 
September 12th 2022 20:51:29Info
Existing IIS bindings do not match configured bindings. 
September 12th 2022 20:51:29Info
Clearing IIS bindings 
September 12th 2022 20:51:29Info
Assigning binding: http *:8024: 
September 12th 2022 20:51:29Info
Anonymous authentication enabled: False 
September 12th 2022 20:51:29Info
Applied configuration changes to section "system.webServer/security/authentication/anonymousAuthentication" for "MACHINE/WEBROOT/APPHOST/OctDeploy" at configuration commit path "MACHINE/WEBROOT/APPHOST" 
September 12th 2022 20:51:29Info
Basic authentication enabled: False 
September 12th 2022 20:51:29Info
Applied configuration changes to section "system.webServer/security/authentication/basicAuthentication" for "MACHINE/WEBROOT/APPHOST/OctDeploy" at configuration commit path "MACHINE/WEBROOT/APPHOST" 
September 12th 2022 20:51:29Info
Windows authentication enabled: True 
September 12th 2022 20:51:30Info
Applied configuration changes to section "system.webServer/security/authentication/windowsAuthentication" for "MACHINE/WEBROOT/APPHOST/OctDeploy" at configuration commit path "MACHINE/WEBROOT/APPHOST" 
September 12th 2022 20:51:30

</td>
</tr>
</table>

12, go to folder C:\Octopus\Applications\development\webapmicro\1.0.0_2 to click .exe file
13, this .net server is running and message will tell you how to open this url in browser such as 

<table><tr><td>
info: Microsoft.Hosting.Lifetime[14]
      Now listening on: http://localhost:5000
info: Microsoft.Hosting.Lifetime[14]
      Now listening on: https://localhost:5001
info: Microsoft.Hosting.Lifetime[0]
      Application started. Press Ctrl+C to shut down.
info: Microsoft.Hosting.Lifetime[0]
      Hosting environment: Production
info: Microsoft.Hosting.Lifetime[0]
      Content root path: C:\Octopus\Applications\development\webapmicro\1.0.0_2\

</td></tr></table>

13, open http://localhost:5000/weatherforecast , you can see the json data is displayed in browser successfully.
