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
Stop-Computer -ComputerName "Host1"
```
Apagar multiples hosts dentro de tu dominio
```powershell
Stop-Computer -ComputerName "HostName", "HostName", "HostName"
```
Apagar un host usando credenciales de administrador
```powershell
Stop-Computer -ComputerName "HostName" -Credential DOMAIN\Administrator
```
Forzar el apagado de un host
```powershell
Stop-Computer -ComputerName "HostName" -Force
```
Reiniciar host
```powershell
Restart-Computer
```
Reiniciar otro host dentro de tu dominio
```powershell
Restart-Computer -ComputerName "HostName"
```

### Cambiar nombre de un host

Obtener el nombre de nuestro host
```powershell
HostName
```
Cambiarle el nombre a tu host
```powershell
Rename-Computer -NewName "HostName"
```
Cambiarle el nombre a otro host usando las credenciales de dominio
```powershell
Rename-Computer -ComputerName "Old_Host_Name" -NewName "New_Host_Name"
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
> En este ejemplo estamos cambiando el valor de 1 a 0 a nuestro archivo **fDenyTSConnections** que se encuentra en nuestra unidad HKLM (HKEY_LOCAL_MACHINE). El número 0 especifica que la conexión de escritorio remoto está habilitado.

> El archivo **fDenyTSConnections** especifica si las conexiones a escritorio remoto están habilitadas.

Habilitar regla de firewall de escritorio remoto
```powershell
Enable-NetFirewallRule -DisplayGroup "Remote Desktop"
```
> El comando **Enable-NetFirewallRule** permite que una regla de firewall previamente deshabilitada esté activa en el equipo o en una unidad organizativa de política de grupo.

Obtener información de nuestra regla de firewall de escritorio remoto
```powershell
Get-NetFirewallRule -DisplayGroup "Remote Desktop"
```
> El comando **Get-NetFirewallRule** devuelve las instancias de reglas de firewall que coinciden con los parámetros de búsqueda del usuario.

Habilitar la regla RDP
```powershell
Set-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP=Tcp" -name "UserAuthentication" -Value 1
```
> RDP (Remote Desktop Protocol, TCP = port 3389) se utiliza para la comunicación entre Terminal Server y Terminal Server Client

### Administración de usuarios y grupos locales

Obtener modulo para la administración de usuarios locales
```powershell
Get-Module Microsoft.PowerShell.LocalAccounts
```
Obtener comandos que se utilizan en el modulo de admnistración de usuarios locales
```powershell
Get-Command -Module Microsoft.PowerShell.LocalAccounts
```
Mostrar usuarios locales
```powershell
Get-LocalUser
```
Mostrar un usuario local en especifico
```powershell
Get-LocalUser -Name LocalUser
```
Agregar usuario local
```powershell
New-LocalUser -Name "UserName" -Description "Type here your description" -NoPassword
```
> En este ejemplo estamos usando el parametro **-NoPassword** que significa que no estamos agregando un password al nuevo usuario

Crear usuario loca utilizando variables
```powershell
$Password = Read-Host "Type your password" -AsSecureString
New-LocalUser "User Name" -Password $Password -FullName "User name fullname" -Description "Type here your description"
```

Eliminar usuario local
```powershell
Remove-LocalUser "User Name"
```
Deshabilitar usuario local
```powershell
Disable-LocalUser "User Name"
```
Habilitar usuario local
```powershell
Enable-LocalUser "User Name"
```
Renombrar usuario local
```powershell
Rename-LocalUser -Name "User Name" -NewName "New user name"
```
Agregar descripción a un usuario local
```powershell
Set-LocalUser -Name "User Name" -Description "Type here your description"
```
Obtener comandos que se utilizan en el modulo de admnistración de grupos locales
```powershell
Get-Command -Module Microsoft.PowerShell.LocalAccounts
```
Mostrar grupos locales
```powershell
Get-LocalGroup
```
Crear un grupo local
```powershell
New-LocalGroup -Name "Group name"
New-LocalGroup -Name "Group name" -Description "Type here your description"
```

Agregar usuarios locales a un grupo local
```powershell
Add-LocalGroupMember -Group "Group name" -Member "User name"
```
Mostrar que usaurios forman parte de un grupo
```powershell
Get-LocalGroupMember -Group "Group name"
```

Eliminar usuario local de un grupo local
```powershell
Remove-LocalGroupMember -Group "Group name" -Member "User name"
```

Eliminar un grupo local
```powershell
Remove-LocalGroup "Group name"
```

Agregar descripción a un grupo local
```powershell
Set-LocalGroup -Name "Group name" -Description "Type here your description"
```

### Administración de servicios

Mostrar todos los servicios
```powershell
Get-Service
```
Mostrar un servicio en especifico
```powershell
Get-Service -Name WinRM
```
Mostrar todos los servicios que empiezan con la palabra **Win**
```powershell
Get-Service -Name "Win*"
```
Mostrar todos los servicios que solamente estan detenidos
```powershell
Get-Service | Where-Object {$_.Status -eq "Stopped"}
```

Detener un servicio
```powershell
Stop-Service -Name "Service Name"
```
### Administración de registros de eventos

Mostrar todos los eventos
```powershell
Get-EventLog -List
```
Mostrar los logs de un evento
```powershell
Get-EventLog -LogName "Event name"
```
Mostrar los 10 primeros logs de un evento
```powershell
Get-EventLog -Newest 10 -LogName Application
```

### Administración de perfiles de firewall
Obneter todos los perfiles de firewall
```powershell
Get-NetFirewallProfile
```
Deshabilitar todos los perfiles de firewall
```powershell
Set-NetFirewallProfile -Enable False
```
Habilitar todos los perfiles de firewall
```powershell
Set-NetFirewallProfile -Enable True
```
Deshabilitar un perfil de firewall en especifico
```powershell
Set-netFirewallProfile -Profile Public -Enable false
```