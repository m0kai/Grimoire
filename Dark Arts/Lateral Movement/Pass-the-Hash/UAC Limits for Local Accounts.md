-- -
User Account Control (UAC) limits local user' ability to do remote administrative tasks. If the reg key `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\LocalAccountTokenFilterPolicy` is set to 0, then only the builtin local admin account (Administrator RID 500) can RDP into the machine, setting it to 1 will allow all local admins to RDP in. 

if `FilterAdministratorToken` is enabled (set to 1), then the builtin local admin account has UAC protection making PTH fail. It is disabled by default. 
