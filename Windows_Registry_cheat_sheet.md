...Updating!...

### HKEY_CURRENT_USER

#### NTUSER.DAT
- Recent Files: `Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs`

- Office Recent Files: `Software\Microsoft\Office\<VERSION>\UserMRU\LiveID_####\FileMRU`

#### USRCLASS.DAT


### HKEY_LOCAL_MACHINE

#### SOFTWARE
- OS version: `Microsoft\Windows NT\CurrentVersion`

- Autostart programs:
  - `Microsoft\Windows\CurrentVersion\Run`
  - `Microsoft\Windows\CurrentVersion\RunOnce`
  - `Microsoft\Windows\CurrentVersion\policies\Explorer\Run`

- Installed Programs:
  - `Microsoft\Windows\CurrentVersion\Uninstall`
  - `WOW6432Node\Microsoft\Windows\CurrentVersion\Uninstall`

#### SYSTEM
- Computer Name: `<CurrentControlSet>\Control\ComputerName\ComputerName`

- Timezone: `<CurrentControlSet>\Control\TimeZoneInformation`

- Network interfaces: `<CurrentControlSet>\Services\Tcpip\Parameters\Interfaces`

- Services: `SYSTEM\CurrentControlSet\Services`

#### SAM
- User information: `Domains\Account\Users`
