Spider (crawler)
================

Locate links
------------

   - In the attributes of selected tags: &lt;a&gt;, &lt;link&gt;, &lt;script&gt;
     etc.

   - In plain text and comments (using regexp)
      - Javascript files often contain links (sometimes using relative paths).
        These links will be verified once inserted into the queue and crawled.
        Only valid links will be stored.
   - robots.txt

Locate input fields
-------------------

   - GET parameters in links.
   - POST parameters in form input fields.
      - Sometimes form entries and input fields are commented out. Look for
        input fields in the comments as well.
   - Cookies:
      - Store cookie names and example values.

Passive information gathering
-----------------------------

   - While crawling, identify known HTTP headers that sometimes contain
     sensitive information.
      - Server, X-AspNet-Version, X-Powered-By, etc.

Queue future requests
---------------------

   - Once a new link is located it can simply be added to the queue.

Eliminate duplicates
--------------------

   - Every part of the crawler should eliminate duplicates early on, preferably
     before they are even crawled.
   - Consider the following example: The spider is multi threaded and uses a
     number of goroutines to crawl pages. The goroutines identify the same link
     on two different pages, and insert them at more or less the same time into
     the queue. The queue itself should be able to recognize duplicates before
     inserting them.

Scope (white list)
------------------

   - It should be possible to specify a white list which limits the scope of the
     crawler. No page should ever be crawled unless it is within the active
     scope.
   - The scope could be controlled using the following:
      - domain name
      - relative path (for a certain domain)
      - file extension

Black list
----------

   - It should be possible to specify a black list, which the crawler will
     consult before actually crawling a page.
   - For instance "logout.php" could be resonable to have in the back list.

Interrupt and resume
--------------------

   - It should be possible to interrupt the crawling of a page and continue on a
     later date.

Results
-------

   - Results should be stored in a well specified manner, so they can be uesd by
     other applications such as a fuzzer or vulnerability scanner.
