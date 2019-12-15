###  This folder has both Notes for the Python tutorial and also the project.

* How do we debug python : https://stackoverflow.com/questions/4929251/how-to-step-through-python-code-to-help-debug-issues

* xrange is slow due to creation of underlying object (of which it is range of) each time it is asked to get the element but it is memory efficient.
    * https://www.geeksforgeeks.org/range-vs-xrange-python/

* iterables which can be iterated upon and iterator are access through next function. generator is a iterator but not all iterators are generators. It has next function lets you not worry about size of the iterator in the beginning of the operation on it. You just have to call next to get next subsequent element and will throw exception if all elements are traversed.

      * https://www.geeksforgeeks.org/python-difference-iterable-iterator/
      * https://stackoverflow.com/a/9884259

* to delete a column and to get the column values into a list 
   ```
   target = df.pop('target')
   ```
   Ideal case for label extraction from pandas in case of supervised learning.

* A quick look on 2 numpy function I came across in a recent program.
   ```
   import numpy as np
   np.array([1,2]).shape, np.expand_dims([1,2], axis=0).shape, np.vstack([np.expand_dims([1,2], axis=0)]).shape
   Output: ((2,), (1, 2), (1, 2))
   ```
* pandas to xls file through xlswriter : https://xlsxwriter.readthedocs.io/example_pandas_chart_stock.html

* datetime function in panda
   * df['time'] = pd.to_datetime(df.time)
   * df.time.dt.day --> lists only day, can be used in groupby
   * df.time.dt.strftime('%d-%b') --> converts to DD-MMM format

* https://www.instagram.com/p/B3Er0pqgJQD/?igshid=frsubx75m40l
* python tools: https://www.datasciencecentral.com/profiles/blogs/7-python-tools-all-data-scientists-should-know-how-to-use

* python does dynamic type checking and hence static type checking is not default. However, the best code practice indicate that type hinting makes the code clearer. And moreover, IDE like PyCharm does enforce typechecking for a safer code.
   ```
   def myFunc(a : int) -> str
      return a
   ```
      * here you might expect the return value is only string but python allows you to send integer back.
      * also you may think that a can be only integer but it might have other too.
      * this is what meant by not enforcing type checking. Hence, it is referred as type hinting and not type checking. 
