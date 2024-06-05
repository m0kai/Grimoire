-- -
#### TTPs
A better approach to discovering exploitable  XSS input field than just inputting `<script>alert(1)</script>`.
1. Pick a dummy payload: `1234'"<t>`
2. Inject payload
3. See **how** it gets reflected in the next page
4. Iterate on the payload until you tweak it to execute Javascript code. 

Key point here is the payload chosen as the start point and the iteration:
1. We include text to see where it lands: `1234`
2. We then include single and double quotes to see how they get interpreted and reflected: `'"`
3. We include a dummy tag to see how that gets processed: `<t>`
This will tell us how the useful symbols will be interpreted and reflected, if anything is encoded or filtered and what we can use to get Javascript to run in a dynamic way.

Submit the payload then search for your string `1234`, see how many times and where the payload shows up in the page source code. Then check how the tag and special characters are impacted. 