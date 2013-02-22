Goal
----
To eliminate purchases caused by "odd prices" and the unnecessary work consumers
make to counteract them.

Will be coded as a firefox extension.

Method
------
Round money on online shopping sites.
  - Adblock like filter
		- http://en.wikipedia.org/wiki/Adblock_Plus
	- Regexp
	- CSS selection

Make all numbers have equal size.
	- Adblock like filter
		- http://en.wikipedia.org/wiki/Adblock_Plus
	- Smaller numbers are unconsciously thought of as less significant

The program should round the price relative to the number of significant digits.
Example:
	- 19 -> 20
	- 199 -> 200
	- 1990 -> 2000

Discussion
----------
Symbol map:
	?	Question/Suggestion
	+	Pro
	-	Con
	!	Info

Should the program mark rounded numbers in red to notify that conversion has
taken place?
	? Optional setting?
	? Hovering the price will show the original value?
	- Could be illegal due to negative feedback against Internet sites?
	- Might be tedious to style all different kinds of notification on many
	pages.

What should the program be called?
	? Maru - in tribute of the round cat that loves boxes.
	? Byteshandel - in tribute of a better currency and since we actually change
	the price (byter) it's connected to the output.
	? Honesty - A more "honest" representation of the price
		- Dislike.
	? Truth - The true price.
		- Dislike.

A method to prevent "Price band" exploitation
	? On JS script sites, changing the values might resolve sorting.
		- This won't work on server-side search queries, though.
			+ Still better than nothing :)

How to prevent lowest possible price misconception?
	! This will be solved when the price is rounded.

Settings
--------

Price rounding equation should be configurable.
	`Settings page is a list of different equations and a table with
	"odd prices" in one column and it's converted prices in another.
	Each time the equation is changed the table will update to show the
	conversion.
	Should be user configurable.
	The user will be warned when a certain percent offset has been reached.`

Research
--------
http://en.wikipedia.org/wiki/Psychological_pricing
