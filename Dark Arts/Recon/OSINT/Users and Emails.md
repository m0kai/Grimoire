-- -
### Tips
1. You can google the `@domain` of the company you are working with for the engagement. So for example, google `@inlanefreight` may give you valid org emails of which the first part `user@company.com` is the AD username of that employee. 
2. You can scrape social media accounts (linkedin profiles of employees) for emails 
3. You can look for PDFs associated with the company that may disclose valid emails you can pull a username from: `inlanefreight.com filetype:pdf`
*Note: Some companies obfuscate their employees usernames via email aliasing where the employee email may be something like a907@inlanefreight that alias to joe.smith@inlanefreight so it's harder to get the joe.smith username from the email.*
### Brute Forcing
If you only get employee names, you can also just generate a list of feasible usernames and just bruteforce something to try to get some valid credentials. 
```bash
# make a list of the employee names, probably fully lowercase. This list will be assumed to be names.txt in the following exampale.
./username-anarchy -i names.txt

# note this is a ruby tool
```