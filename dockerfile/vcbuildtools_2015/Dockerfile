FROM mcr.microsoft.com/windows/servercore:1909

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

RUN Invoke-WebRequest 'http://download.microsoft.com/download/5/f/7/5f7acaeb-8363-451f-9425-68a90f98b238/visualcppbuildtools_full.exe' -OutFile 'visualcppbuildtools_full.exe' -UseBasicParsing ; \
    Start-Process .\visualcppbuildtools_full.exe -ArgumentList '/NoRestart /S' -Wait ; 

RUN Write-Host 'Configuring environment'; \
	pushd 'C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC' ; \
	cmd /c 'vcvarsall.bat amd64&set' | foreach { \
    if ($_ -match '=') { \
      $v = $_.split('='); \
      [Environment]::SetEnvironmentVariable($v[0], $v[1], [EnvironmentVariableTarget]::Machine); \
    } \
  } ; \
	popd

WORKDIR /code
