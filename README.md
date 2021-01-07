# DockerServer


# Instalar característica Containers y reiniciar
Install-WindowsFeature containers
Restart-Computer -Force

# Descargar, instalar y configurar Docker Engine
Invoke-WebRequest "https://download.docker.com/components/engine/windows-server/cs-1.12/docker.zip" -OutFile "$env:TEMP\docker.zip" -UseBasicParsing

Expand-Archive -Path "$env:TEMP\docker.zip" -DestinationPath $env:ProgramFiles

# Para uso rápido. no necesita reiniciar
$env:path += ";c:\program files\docker"

# para uso persistente, necesita reiniciar 
[Environment]::SetEnvironmentVariable("Path", $env:Path + ";C:\Program Files\Docker", [EnvironmentVariableTarget]::Machine)

# registrar Servicio e iniciarlo
dockerd --register-service
Start-Service docker


[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12


Invoke-WebRequest "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-Windows-x86_64.exe" -UseBasicParsing -OutFile $Env:ProgramFiles\Docker\docker-compose.exe
