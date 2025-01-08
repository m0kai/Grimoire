-- -
Pass-the-Hash attacks.
### RDP
`Restricted Admin Mode` needs to be enabled on the system. It is disabled by default. To enable it, you need to set the registry key `DisableRestrictedAdmin` under `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Lsa`. You can do so visually using the `Registry Editor` or with the following command in cmd or powershell:
```powershell
reg add HKLM\System\CurrentControlSet\Control\Lsa /t REG_DWORD /v DisableRestrictedAdmin /d 0x0 /f
```
Then PtH away!
![[RDP#^062e8b]]
