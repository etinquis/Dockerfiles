# escape=`

FROM mcr.microsoft.com/windows/servercore:ltsc2019

SHELL ["cmd", "/S", "/C"]

ADD https://aka.ms/vs/17/release/channel C:\TEMP\VisualStudio.chman
ADD https://aka.ms/vs/17/release/vs_buildtools.exe C:\TEMP\vs_buildtools.exe

RUN C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache `
    --channelUri C:\Temp\VisualStudio.chman `
    --installChannelUri C:\Temp\VisualStudio.chman `
    --add Microsoft.VisualStudio.Workload.VCTools;includeRecommended `
    --add Microsoft.VisualStudio.Component.VC.Tools.x86.x64 `
    --add Microsoft.VisualStudio.Component.VC.140 `
|| IF "%ERRORLEVEL%"=="3010" EXIT 0

ADD https://chocolatey.org/install.ps1 C:\TEMP\install.ps1
RUN @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex C:\Temp\install.ps1"

RUN cinst windows-sdk-8.1 -y

ARG CMAKE_VERSION=3.23.2
ARG SWIG_VERSION=4.0.2.04082020

RUN cinst cmake -version %CMAKE_VERSION% --installargs 'ADD_CMAKE_TO_PATH=User'  -y
RUN cinst swig -version %SWIG_VERSION%  -y

RUN cmake --version
RUN swig -version

ENTRYPOINT ["C:\\Program Files (x86)\\Microsoft Visual Studio\\2022\\BuildTools\\Common7\\Tools\\vsdevcmd.bat", "&&", "powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]