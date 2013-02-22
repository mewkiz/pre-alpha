Vulnerability scanner
=====================

Scan for the following vulnerabilities
--------------------------------------

   - XSS
   - SQL injection (without harmful queries)
   - CRLF injection (HTTP response splitting)
   - Session fixation
   - LFI
   - etc.
   - Create links to exploit-db

Usable characters (for injection purposes)
------------------------------------------
   - Make injection map with similar interface to:
      - http://jisho.org/kanji/radicals/
	- or as a charset:
		- abcdefghijklmnopqrtstuvwxyz'";
	- or as regexp charset:
		- [A-z!']
