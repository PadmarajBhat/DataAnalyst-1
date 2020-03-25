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
   
* u'' is like raw'' for a string. It indicates that the strings character has to be saved as unicoded. The advantage of doing unicoded string is that it consumes less space. Note that u'hello' == "hello", https://stackoverflow.com/a/11279428 ( or even detailed explanation at https://docs.python.org/3/howto/unicode.html ) 
   def myFunc(a : int) -> str
      return a
   ```
      * here you might expect the return value is only string but python allows you to send integer back.
      * also you may think that a can be only integer but it might have other too.
      * this is what meant by not enforcing type checking. Hence, it is referred as type hinting and not type checking. 
      
* ``` pip freeze > requirements.txt``` : it saves your life by helping you to capture the current version of the packages required for the current server(py program) run. Along with code this is the important piece of code should go to checkin. It is kind of saving image in a cloud. You can use this file for recreating the environment used for dev and replicate the same in prod. However, if you are building the one year old project then it might happen that those packages are lost/not supported and you might not be able to recreate the env. In this case an image has upper hand as it is ready to launch environment. In case of image also upper or lower stack for the image might have lost support like operating system might no longer support some api calls (lower stack) and ui might have enhanced to send additional header and requires backend change(upper stack)

* Good example of map, filter and reduce
   ```
   def mapfunc(x):
    return(x*2)

   def filterFunc(x):
       return 0
   a = [1,2,3,4,-1]

   print(list(map(lambda x : mapfunc(x), a)))


   print(list(filter(lambda x: mapfunc(x) , a)))

   print(list(filter(lambda x: filterFunc(x) , a)))

   import functools as fn
   print(fn.reduce(lambda x,y: x if x < y else y, a))
   ```
   Output:
   ```
   [2, 4, 6, 8, -2]                                                                                                                              
   [1, 2, 3, 4, -1]                                                                                                                              
   []                                                                                                                                            
   -1  
   ```

* what if you dont want to use lambda func ?
   ```
   def mapfunc(x):
    return(x*2)
    
   def filterFunc(x):
       return 0

   def whoIsMax(ref, x):
       if ref > x:
           return ref
       return x


   a = [1,2,3,4,-1]

   print(list(map(mapfunc, a)))


   print(list(filter(mapfunc , a)))

   print(list(filter(filterFunc, a)))

   import functools as fn
   print(fn.reduce(lambda x,y: x if x < y else y, a))

   print( fn.reduce(whoIsMax,a))

   print(fn.reduce(mapfunc,a))
   ```
   Output:
   ```
   [2, 4, 6, 8, -2]                                                                                                                                
   [1, 2, 3, 4, -1]                                                                                                                                
   []                                                                                                                                              
   -1                                                                                                                                              
   4                                                                                                                                               
   Traceback (most recent call last):                                                                                                              
     File "main.py", line 38, in <module>                                                                                                          
       print(fn.reduce(mapfunc,a))                                                                                                                 
   TypeError: mapfunc() takes 1 positional argument but 2 were given                                                                        ```
   * This is because the definition of the the three indicates the first argument as function
      ```
      https://docs.python.org/3/library/functools.html
      functools.reduce(function, iterable[, initializer])
      ```
     * a quick recap : https://towardsdatascience.com/top-3-python-functions-you-dont-know-about-probably-978f4be1e6d
     
* interesting discuss on map and list comprehension: more towards list comprehension than map 
   * https://stackoverflow.com/a/1247490/8693106
   * it has to be clear that map is the winner over for loop when operation on indivisual items are not related to each other
      * https://www.quora.com/What-is-the-use-of-the-map-function-in-Python
* Decorator and meta classes are called as meta programming
   * beautiful line from a medium blog : https://medium.com/better-programming/meta-programming-in-python-7fb94c8c7152
      * Meta programming is an act of writing a code to manupulate the code !!!!
   * http://book.pythontips.com/en/latest/decorators.html gives the 2 use cases of meta programming
      * authentication
      * logging

* Medium blog study : https://levelup.gitconnected.com/faster-lists-in-python-4c4287502f0a
   * there are 3 ways lists can be created in python : preallocation, append and list comprehension
      * list comprehension is the fastest > append > preallocation
   * Searching in the set (ordered list) is the fastest way of search > ```in``` search > for loop search
   * timsort is the fastest way to sort the list: list_a.sort() is the builtin available.
   

* Medium blog study: https://towardsdatascience.com/ultimate-setup-for-your-next-python-project-179bda8a7c2c
   * talks about the python code hierarchy study: best practice to include every aspect coding, building, CI/CD, test script and automation.
      * There are 7 files and 3 folders for this project template
      * Folders:
         * blueprint: app name instead of blueprint
            * __init__.py : for indicating it is python package
            * __main__.py: to be able to run python -m blueprint
               * -m takes package as argument
            * app.py: represents set of files in real application where business logic is distributed among modules.
            * resources: this sub directory holds the static files likes png, key files, images etc
         * test: test suite related files
         * .github: folder contains
            * build-test.yaml : building, testing, linting source code
            * push.yaml: to push the code to github registry
         * Makefile: automated scripts for clean building, testing, linting etc
         * configure_project.sh : quick script which will rename dummy values in the project. name of the package or project etc

* Does Python have constants : https://medium.com/better-programming/does-python-have-constants-3b8249dc8b7b
   * awesome comments : dataclass and Enum provide ways to make constants in python
   * Dataclass:
      ```
      from dataclasses import dataclass
      @dataclass(frozen=True)
      class Consts:
        RATIO_LB_TO_KG = 3.281
        RATIO_FEET_TO_METERS = 2.205
      myconsts = Consts()
      myconsts.RATIO_FEET_TO_METERS = 1 # generates an error
      ```
   * Enum:
   ```
   from enum import Enum
   class abcd(Enum):
      a = 20
      
   abcd.a = 30 # generates error : raise AttributeError('Cannot reassign members.')
   ```
* RxPy: is similar to RxJS for js. You can create observables to send continuous stream of data.
* https://docs.djangoproject.com/en/3.0/ref/request-response/#django.http.StreamingHttpResponse: splits a request into smaller chunks but not streaming  

* Bokeh : https://docs.bokeh.org/en/latest/docs/user_guide/categorical.html?highlight=panda#pandas
   * have the entire example as a function and pass df to it. Cant think of cyl_mg example not fitting any case !!!!!

* panda : skew() is Normalized making it handly for any series
   * skewness is said to be stable if the range is -.5 to .5
   * skewness 0.5 to 1 (+-) then it is moderately distributed
   * and within 0.5 is is symmetric 
   * it also to be known that negative sign indicates that the density is of the data points are the right or long tail at left
   * similarly positive sign indicates density at the left or  long tails at right
* number to string : "{:03d}".format(100)

* ternary operation : var = true_val if condition else false_val
* boxplot in matplotlib : https://pythonprogramminglanguage.com/statistics/
   * it is been all the line and scatter but from the 5 point summary sake box plot actually summarizes the view nicely

* KDE: https://mathisonian.github.io/kde/
   * how kernel density works to calculate the probability of the data points to a distribution
   * what are their parameters   

* to search in series: "a" in series.tolist() or "a" in series.values() : https://stackoverflow.com/questions/21319929/how-to-determine-whether-a-pandas-column-contains-a-particular-value

* how to subtract time: datetime.datetime.now() - datetime.deltatime(days=4) : https://stackoverflow.com/a/20573492/8693106

* and /or condition in Panda : https://stackoverflow.com/a/22591267/8693106 - df[(df.a ==1) & (df.b == 2)]
* to get the week number from datetime: date.isocalendar()
* **nonlocal** : to use the parent function variable where the current function definition present 
* panda groupby can have grouper which can easily group datetime to month, quarter or 2 years group
   * https://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html#dateoffset-objects
      * B : indicates the business day
         * if I say 5B then it would mean 5 days from the last date of the panda at current scope.
      * D : indicates the calendar day
         * if I say 5D then it would mean in that calender week 5 days from the **beginning** of the panda data at scope
      * even with these features, I had to write a for loop to get the year wise slicing of time range.

* to search anywhere in panda : https://stackoverflow.com/a/24665721/8693106

* pydrive to access gdrive : https://stackoverflow.com/a/40625642/8693106
   * to search in a folder, folder id has to be given
   
* pydrive: GetContentFile - helps to download file
* tried various ways of authentication but of no sucess
   * gauth.LoadCredentialsFile("credentials.json") dint work
   * need to find something from : https://www.programcreek.com/python/example/93082/pydrive.auth.GoogleAuth
   * also trying to see how pygsheet works at https://github.com/nithinmurali/pygsheets/blob/staging/pygsheets/authorization.py
      * client_secret = kwargs.get('outh_file', client_secret) : I think this is key
      * credentials = service_account.Credentials.from_service_account_file(service_account_file, scopes=scopes)
      
* panda to list of dictionary : .to_dictionary("records")
* **column same hack**: I accidentally had same column names in a panda....One in the beginning and one at the end. I got rid of the first with df.iloc[:,1:]
* **how to do multiple column update**: https://stackoverflow.com/questions/32603051/pandas-dataframe-how-to-update-multiple-columns-by-applying-a-function

* Interesting Read: https://medium.com/swlh/making-data-trees-in-python-3a3ceb050cfd
   * https://treyhunner.com/2018/10/asterisks-in-python-what-they-are-and-how-to-use-them/#Asterisks_in_list_literals: Use of *
      * it can be used to put in all the items in both list or dictionary
      * it is syntactical sugar to reduce the trivial code
      * the difference between * and : operator
         * "*" would all the elements in the current list
         * ":" would add the current list as the element inside a list
         * list of list vs list of elements
         ```
         a = [1,2,3,4,5]
         print([*a[2:],[a[2:])
         [3, 4, 5], [[3, 4, 5]]
         ```
* reset_index : has drop= and when set with True removes the index column introduced due to merge or concatenation

* panda range: sample of records of every year between 2 dates
   * should it have month and date consideration? Like first filter all the records by date and month and then group by year?
   * https://stackoverflow.com/questions/25864133/pandas-groupby-date-range dint help
   * https://stackoverflow.com/questions/54776538/group-by-date-range-in-pandas-dataframe dint help
   * https://www.shanelynn.ie/summarising-aggregation-and-grouping-data-in-python-pandas/ no help
   
* compute business days between 2 dates :
   * https://stackoverflow.com/questions/3615375/count-number-of-days-between-dates-ignoring-weekends
   * https://stackoverflow.com/questions/54435328/numpy-typeerror-could-not-be-cast-from-dtypem8us-to-dtypem8d
   ```
   start_time = datetime.datetime(2020, 3, 18, 7, 9, 9, 453273)
   end_time = datetime.datetime.now()

   print(type(start_time), type(end_time))
   print(np.busday_count(start_time.date(),end_time.date()))
   Output:
   <class 'datetime.datetime'> <class 'datetime.datetime'>
   4
   ```
      * need to add 1 to include the border days
* max column: https://stackoverflow.com/a/29919489/8693106
