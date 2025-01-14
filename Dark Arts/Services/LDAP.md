-- -
### windapsearch
```bash
# --da: enumerate domain admins
windapsearch.py --dc-ip [dc ip] -u [user]@[domain] -p [passwd] --da

# -PU: enumerate privileged users, i.e. users with excess privs from nested group membership
windapsearch.py --dc-ip [dc ip] -u [user]@[domain] -p [passwd] -PU
```

^1a54ad
