text_histogram
==============

|version| |downloads|

Histograms are great for exploring data, but numpy and matplotlib are heavy and
overkill for quick analysis. They also can't be easily used on remote servers
over ssh. Don't even get me started on installing them.

`Bit.ly's data_hacks <https://github.com/bitly/data_hacks>`_ histogram.py is
great but difficult to use from python code directly (it requires an
``optparse.OptionParser`` to pass histogram options). This is histogram.py
repackaged for convenient script use.

::

    Python 3.11.3 (tags/v3.11.3:f3909b8, Apr  4 2023, 23:49:59) [MSC v.1934 64 bit (AMD64)] on win32
    Type "help", "copyright", "credits" or "license" for more information.
    >>> from text_histogram import histogram
    >>> histogram([1, 2, 2, 2, 2, 3, 3, 3], graph_char='#')
    # NumSamples = 8; Min = 1.00; Max = 3.00
    # Mean = 2.250000; Variance = 0.437500; SD = 0.661438; Median 2.000000
    # each # represents a count of 1
         1.0000 -      1.2000 [     1]: #
         1.2000 -      1.4000 [     0]:
         1.4000 -      1.6000 [     0]:
         1.6000 -      1.8000 [     0]:
         1.8000 -      2.0000 [     4]: ####
         2.0000 -      2.2000 [     0]:
         2.2000 -      2.4000 [     0]:
         2.4000 -      2.6000 [     0]:
         2.6000 -      2.8000 [     0]:
         2.8000 -      3.0000 [     3]: ###
    >>> histogram([1, 2, 2, 2, 2, 3, 3, 3], graph_char='#', display_empty_buckets=False)
    # NumSamples = 8; Min = 1.00; Max = 3.00
    # Mean = 2.250000; Variance = 0.437500; SD = 0.661438; Median 2.000000
    # each # represents a count of 1
         1.0000 -      1.2000 [     1]: #
         1.8000 -      2.0000 [     4]: ####
         2.8000 -      3.0000 [     3]: ###


Installation
============

.. code:: bash

    pip uninstall text_histogram text_histogram3  # avoid conflicts
    pip install text_histogram32


Source: https://github.com/clach04/text_histogram32

Fork of https://github.com/Kobold/text_histogram with a few tweaks:

  * **Same** name space as original text_histogram
  * Python 3 and 2.7 support
  * Support for control over character used for the bar (see `graph_char` and `DEFAULT_graph_char` option)
  * Support for NOT displaying empty buckets/bins/intervals (see `display_empty_buckets` and `DEFAULT_display_empty_buckets` option)
  * Fixes
      * https://github.com/Kobold/text_histogram/issues/4 - Zero for min or max value
      * when min == max value
      * improved error handling for empty data sets

ToDo items

  * Test suite
  * see https://github.com/piccolomo/plotext/blob/master/readme/bar.md#histogram-plot
  * see https://github.com/nschloe/termplotlib?tab=readme-ov-file#similar-projects
  * Improve dynamic sizing of string and bar
  * Support for non-linear buckets/bins/intervals (see `display_empty_buckets` option)?
  * Support for Scott's rule https://en.wikipedia.org/wiki/Scott%27s_rule ?
  * Bug? https://github.com/Kobold/text_histogram/issues/2 https://github.com/bitly/data_hacks/pull/22
  * Bug different results for python 2 (missing bar) compared with Python 3 - test case below:

::

    from text_histogram import histogram
    python2_3_difference_with_low_counts = []

    python2_3_difference_with_low_counts += [  2540] *  1142
    python2_3_difference_with_low_counts += [  5071] *   163
    python2_3_difference_with_low_counts += [  7602] *    67
    python2_3_difference_with_low_counts += [ 10134] *    28
    python2_3_difference_with_low_counts += [ 12665] *    17
    python2_3_difference_with_low_counts += [ 15196] *    14
    python2_3_difference_with_low_counts += [ 17728] *     4
    python2_3_difference_with_low_counts += [ 20259] *     4
    python2_3_difference_with_low_counts += [ 22790] *     2
    python2_3_difference_with_low_counts += [ 25322] *     4
    python2_3_difference_with_low_counts += [ 27853] *     2
    python2_3_difference_with_low_counts += [ 30384] *     4
    python2_3_difference_with_low_counts += [ 32915] *     2
    python2_3_difference_with_low_counts += [ 40509] *     2
    python2_3_difference_with_low_counts += [ 45572] *     1
    python2_3_difference_with_low_counts += [ 50635] *     1
    python2_3_difference_with_low_counts += [ 55697] *     1
    python2_3_difference_with_low_counts += [ 63291] *     1
    python2_3_difference_with_low_counts += [129105] *     1
    python2_3_difference_with_low_counts += [162012] *     1
    python2_3_difference_with_low_counts += [253139] *     1

    print(python2_3_difference_with_low_counts)

    histogram(python2_3_difference_with_low_counts, buckets=100, graph_char='#', display_empty_buckets=False)



.. |downloads| image:: https://pypip.in/d/text-histogram32/badge.png
   :target: https://pypi.python.org/pypi/text-histogram32
   :alt: Number of PyPI downloads
.. |version| image:: https://badge.fury.io/py/text-histogram32.png
   :target: http://badge.fury.io/py/text-histogram32
   :alt: PyPI version
