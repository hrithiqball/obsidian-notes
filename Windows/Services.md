> Command for Windows Services

```powershell
# for help
sc /?

# for creating new service; name != displayname
sc create vms-service displayname= "VMS service" type= own error= severe binpath= "C:\path\to\bin\vmsservice.exe"

# for delete
sc delete vms-service

# to view the config and info of a service
sc config vms-service

# to add description for a service
sc description vms-service "This is a description for a service"
```
