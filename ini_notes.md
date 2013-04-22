ini
===

Implementation notes and ideas:

* Support both read and write functionality. It should be possible to add and
  remove both sections and keys.
* Parse *all* data so it can be written back in a normalized format. This
  includes comments.
* Don't use default values, instead use the "comma ok" idiom.
