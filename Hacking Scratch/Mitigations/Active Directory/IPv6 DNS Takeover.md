-- -
1. If the org only uses IPv4 traffic and does not use IPv6 for anything, the best and easiest way to mitigate MITM over IPv6 is to just block DHCPv6 traffic altogether. You can block this traffic in the Windows firewall via a Group Policy. Some key settings to block:
	1. (Inbound) Core Networking - Dynamic Host Configuration Protocol for IPv6 (DHCPv6-In)
	2. (Inbound) Core Networking - Router Advertisement (ICMPv6-In)
	3. (Outbound) Core Networking - Dynamic Host Configuration Protocol for IPv6 (DHCPv6 - Out)
2. If WPAD is not in use internally, disable it via Group Policy and by disabling the WinHttpAutoProxySvc Service.
3. Relaying to LDAP/LDAPS can be mitigated by enabling LDAP signing and LDAP channel binding.
4. Consider adding Administrative accounts to the Protected Users group or marking them as Account is sensitive and cannot be delegated. 