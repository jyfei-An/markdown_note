FROM mcr.microsoft.com/dotnet/framework/sdk:4.8-windowsservercore-ltsc2019

ADD https://aka.ms/vs/15/release/vs_buildtools.exe C:\\TEMP\\vs_buildtools.exe

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

RUN	Start-Process -Wait -NoNewWindow C:\TEMP\vs_buildtools.exe -ArgumentList "--quiet", "--wait", "--norestart", "--installPath=C:\BuildTools", \
	"--add=Microsoft.VisualStudio.Workload.VCTools", "--includeRecommended", "--add=Microsoft.VisualStudio.Component.VC.ATL"