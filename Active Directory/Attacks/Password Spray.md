-- -
Try to log into multiple accounts with one password, so roll through a wordlist of usernames trying a single password, or a small list of passwords, for each username. This technique is common in AD since there will be a password policy that's enforced and there will be a password lockout policy to stop standard bruteforce attacks. 
### TTP
1. Try to get the organization's [[Password Policy]]
2. Build a list of valid [[Username Enumeration|usernames]]
3. Come up with spray plan (how many attempts over what time period and with a delay)
4. Spray within the plan