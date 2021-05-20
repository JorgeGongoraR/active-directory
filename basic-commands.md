# Active Directory

Aplicaciones graficas que existen en un servidor core

- Notepad
- Regedit
- Taskmng
- Msiexec
- Msinfo32.exe

Cmdlets (comandos)

Obtener información de nuestro powershell
```powershell
Get-Host
```
Mostrar una lista de los modulos que estan listos para administrar en nuestro host
```powershell
Get-Module -ListAvailable
```
Mostrar que comandos se pueden utilizar en un modulo
```powershell
Get-command -Module <Module_Name>
```

### Apagar y reiniciar un host

Apagar tu host
```powershell
Stop-Computer
```
Apagar otro host dentro de tu dominio
```powershell
Stop-Computer -ComputerName "Server1"
```
Apagar multiples hosts dentro de tu dominio
```powershell
Stop-Computer -ComputerName "Server1", "Server2", "Server3", "ServerN"
```
Apagar un host usando credenciales de administrador
```powershell
Stop-Computer -ComputerName "Server1" -Credential DOMAIN\Administrator
```
Forzar el apagado de un host
```powershell
Stop-Computer -ComputerName "Server1" -Force
```
Reiniciar host
```powershell
Restart-Computer
```
Reiniciar otro host dentro de tu dominio
```powershell
Restart-Computer -ComputerName "ServerName"
```

### Cambiar nombre de un host

Obtener el nombre de nuestro host
```powershell
HostName
```
Cambiarle el nombre a tu host
```powershell
Rename-Computer -NewName "ServeName"
```
Cambiarle el nombre a otro host usando las credenciales de dominio
```powershell
Rename-Computer -ComputerName "Old_Server_Name" -NewName "New_Server_Name"
-DomainCredential DOMAIN\User
```

### Configurar fecha, hora y zona horaria

Obtener fecha de nuestro host
```powershell 
Get-Date
```
Agregar tres días a la fecha de nuestro host
```powershell
Set-Date -Date (Get-Date).AddDays(3)
```
Quitar tres días a la fecha de nuestro host
```powershell
Set-Date -Date (Get-Date).AddDays(-3)
```
Agregar tres horas a la hora actual de nuestro host
```powershell
Set-Date -Date (Get-Date).AddHours(3)
```
Quitar tres horas a la hora actual de nuestro host
```powershell
Set-Date -Date (Get-Date).AddHours(-3)
```
Retroceder la hora actual de nuestro host en 10 minutos.
```powershell
Set-Date -Adjust -0:10:0 -DisplayHint Time
```
Mostrar la zora horaria de nuestro host
```powershell
tzutil /g
```
Mostrar todas las zonas horarias disponibles
```powershell
tzutil /l | more
```
Establecer nueva zona horaria
```powershell
tzutil /s "Zone Name" 
```

### Habilitar escritorio remoto y reglas de firewall

Cambiar el valor a una archivo de reistro
```powershell
Set-ItemProperty -Path "HKLM:\system\CurrentControlSet\Control\Terminal Server" -name "fDenyTSConnections" -value 0
```
> En este ejemplo estamos cambiando el valor a nuestro archivo **fDenyTSConnections** que se encuentra en nuestra unidad HKLM (HKEY_LOCAL_MACHINE). 

> El archivo **fDenyTSConnections** especifica si las conexiones a escritorio remoto están habilitadas.
 