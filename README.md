# ocpr, a tool for verifying if a pull request or cherry pick has been integrated in an OCP release or not

with the bunch of requests being added to an OCP release, it's hard to track if a certain patch made it into a release or not.
Giving that we do have release notes we can look in, it might still get quickly uncomfortable to tell, if and when (which release).

This tool is ment to fetch and parse all available OCP release notes and do that for us.

ToDo:

* wildcard searches like "any fix with '.*volume.*' in the commit message (and similar)

## install

Requirements:

* python >= 3.8
* requests
* lxml
* BeautifulSoup

```
pip3 install --user requests lxml BeautifulSoup
```

## simple verification is my cherry pick integrated or not

Requirements:

* some kind of unique identified (even though matching is done through regex, false/positives might show)
* the base version and channel you want to verify 
	* channels: stable,candidate,fast
	* versions: 4.9, 4.10, 4.11, 4.12

## detailed verification is my cherry pick integrated or not and which versions

Requirements:

* some kind of unique identified (even though matching is done through regex, false/positives might show)
* the base version and channel you want to verify
        * channels: stable,candidate,fast
        * versions: 4.9, 4.10, 4.11, 4.12


### example verification 

Is my cherry pick with the commit message "When volume is not marked" included in 4.9 stable channel ?

```
./ocpr -v 4.9 -c stable -s 'When volume is not marked'
stable-4.9 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391

```

### example detailed verification

Is my cherry pick with the commit message "When volume is not marked" included in 4.9 stable channel and in which release versions ?

```
./ocpr -v 4.9 -c stable -s 'When volume is not marked' --which 
4.9.30 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.31 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.33 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.34 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.35 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.36 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.37 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.38 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.39 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.40 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.41 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.42 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.43 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.44 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.45 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.46 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.47 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.48 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.49 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.50 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.51 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.52 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.53 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.54 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
4.9.55 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
stable-4.9 Found: Automated cherry pick of #106853: When volume is not marked in-use, do not backoff #107391
```
