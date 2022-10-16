## IDOR Example: Direct Database Reference[](https://highon.coffee/blog/insecure-direct-object-reference-idor/#idor-example-direct-database-reference)

A typical numeric IDOR vulnerable function would look like:

```bash
foo.com/profile/user_id=7747
```

If the `user_id` parameter is vulnerable to IDOR an attacker could simply modify the numeric value and access another users profile. If successful an attacker could gain access to a user acverticalcount profile and potentially perform horizontal, or vertical privilege escalation against the vulnerable application.

## IDOR Example: File Name[](https://highon.coffee/blog/insecure-direct-object-reference-idor/#idor-example-file-name)

Another typical example of an IDOR vulnerability would be file names with a predictable value that could be bruteforced, guessed or predicted if sequential, such as:

```bash
foo.com/download/12432-secure-document.pdf 
```

If the file name is vulnerable to IDOR an attacker could simply predict or bruteforce the numeric value and access another users file. If successful an attacker could potentially gain access to the document.

## How To Find IDOR Vulnerabilties[](https://highon.coffee/blog/insecure-direct-object-reference-idor/#how-to-find-idor-vulnerabilties)

This document walks through some potential techniques on how to find IDOR vulnerabilities witin vulnerable web applications. Due to the manual process of building and implimenting access control systems, mistakes could be made (human error). Unfortunately, identifying IDOR vulnerabilities is typically best done manually.

## IDOR Entry Points[](https://highon.coffee/blog/insecure-direct-object-reference-idor/#idor-entry-points)

Assess the application for predictable parameters or URL’s, some food for thought:

1.  Profile URL’s or ID’s
2.  Password reset functions (great for privilege escalation)
3.  Numeric parameters
4.  Predictable parameters

```bash
foo.com/profile/user_id=7747
```

If the `user_id` parameter is vulnerable to IDOR an attacker could simply modify the numeric value and access another users profile. If successful an attacker could gain access to a user acverticalcount profile and potentially perform horizontal, or vertical privilege escalation against the vulnerable application.

## IDOR Example: File Name[](https://highon.coffee/blog/insecure-direct-object-reference-idor/#idor-example-file-name-1)

Another typical example of an IDOR vulnerability would be file names with a predictable value that could be bruteforced, guessed or predicted if sequential, such as:

```bash
foo.com/download/12432-secure-document.pdf
```

If the file name is vulnerable to IDOR an attacker could simply predict or bruteforce the numeric value and access another users file. If successful an attacker could potentially gain access to the document.

## Finding Access Control Bug (IDOR)[](https://highon.coffee/blog/insecure-direct-object-reference-idor/#finding-access-control-bug-idor)

You could argue that strictly speaking this is not an IDOR bug, however (call it what you want to call it), either way it is still an issue.

1.  Using BurpSuite or another similar tool, browse the application as a user or ideally a privileged user account
2.  Authenticate as another user account, or an account with lower priveleges - and obtain a session identifier (token/cookie)
3.  Use the session identifier obtained during step 2 against the URL’s from step 1

##### Web Server Response Codes Lie

Do not depend solely on response codes, many web applications respond with incorrect response codes.

## IDOR vs Forced Browsing: What’s the Difference?[](https://highon.coffee/blog/insecure-direct-object-reference-idor/#idor-vs-forced-browsing-whats-the-difference)

Forced browsing and IDOR vulnerabilties are very similar access control vulnerabilities. The main thing that seperates the vulnerabilties is the method of discovery is typically bruteforcing URL’s for forced browsing e.g. with a large word list and IDOR detection is typically discovered by brute forcing predicatable parameters.