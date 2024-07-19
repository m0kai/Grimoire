-- -
Ways to breach AD. This area is on notes for when you find yourself in an AD environment, but do not yet have any valid credentials. These vectors are all from an unauthenticated perspective and for trying to get an account when you do not have any others. You can obviously do this after you have a valid account, but in general, for initial compromise/foothold into the AD network. 
### Strats
General strategy to get those initial credentials in AD that allow you to borrow deeper into the network. 
[[Dark Arts/Active Directory/Initial Breach/TTPs]]

### Man-In-The-Middle
These vectors generally rely on putting yourself on the network in a way that users will go to you and hand you authentications that you can then crack or relay or #pass-the-hash.
[[LLMNR Poisoning]]
[[SMB Relay]]
[[Dark Arts/Active Directory/Initial Breach/IPv6 DNS Takeover|IPv6 DNS Takeover]]
[[Passback Attack]]
