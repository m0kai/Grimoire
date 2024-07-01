-- -
Ways to find out which users have RDP access on which hosts. Some hosts may allow RDP from anyone or some users may have access to some hosts.
#### Powerview
![[PowerView (depricated)#^75452d]]
#### Bloodhound
1. Select a `Node` and go to: `Node Info`->`Execution RIghts`
2. Select the `Analysis` tab. Run pre-built query: `Find Workstations where Domain USers can RDP` or `Find Servers where Domain Users can RDP`.