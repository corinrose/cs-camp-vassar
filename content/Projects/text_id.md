---
title: "Text ID"
date: 2018-07-13T10:56:09-04:00
draft: false
---


This project offers you an opportunity to use Python to develop a statistical model of text that will allow you to "ID" an author or style---with varying degrees of success---from samples of text!

Background
----------

Statistical models are one way to quantify how similar one piece of text is to another. Such models were used as evidence that the book The Cuckoo's Calling was written by J. K. Rowling (using the name Robert Galbraith) in the summer of 2013. Details on that story and the analysis done [appear at this link](https://www.salon.com/2013/08/23/how_j_k_rowling_was_exposed_as_robert_galbraith_partner/).

The comparative analysis of those works used simple models---perhaps surprisingly simple---of an "author's style," for example, the distribution of word lengths in a document. The five "text features" that we ask you to implement for this project are:

- The distribution of words used by an author.
- The distribution of word lengths (noted above).
- The distribution of word stems used (e.g., "spam" and "spamming" would have the same stem).
- The distribution of sentence lengths used.
- Plus, the project asks you to include one more "text feature" of your own design:
  - For example, you could use punctuation in some way.
  - Or you could compute something else about the text---it could be the number of words ending in "ness," something about capitalization, or anything else you can compute or count using Python... 
- [Here is an article](http://mentalfloss.com/article/75602/what-famous-novels-look-stripped-everything-punctuation) on the punctuation analysis of several works... 

Perhaps the most-common and most-successful application of this kind of textual analysis is Spam detection and filtering. 

Overview of the `TextModel` project
-----------------------------------

To create your Bayesian classifier (which is what this project is!) you will create `TextModels`, which will be lists of dictionaries. Each of these lists should have at least five dictionaries. Here is some starter code that creates a single model with the following four dictionaries, initially empty:

- `words`
- `wordlengths`
- `stems`
- `sentencelengths`
- Remember that you'll need one more dictionary for a text feature of your own design! Punctuation is totally ok, as are many other options. 

Feel free to start with this:

~~~text
#
# textmodel.py
#
# TextModel project!
#
# Name(s):
#

class TextModel(object):
    """A class supporting complex models of text."""

    def __init__(self):
        """Create an empty TextModel."""
        #
        # Create dictionaries for each characteristic
        #
        self.words = {}           # For counting words
        self.wordlengths = {}     # For counting word lengths
        self.stems = {}           # For counting stems
        self.sentencelengths = {} # For counting sentence lengths
        #
        # Create another of your own
        #
        self.myparameter = {}     # For counting ___________

    def __repr__(self):
        """Display the contents of a TextModel."""
        s = 'Words:\n' + str(self.words) + '\n\n'
        s += 'Word lengths:\n' + str(self.wordlengths) + '\n\n'
        s += 'Stems:\n' + str(self.stems) + '\n\n'
        s += 'Sentence lengths:\n' + str(self.sentencelengths) + '\n\n'
        s += 'MY PARAMETER:\n' + str(self.myparameter)
        return s

    # Include other functions here.
    # In particular, you'll need functions that add to the model.

# And test things out here...
TM = TextModel()
# Add calls that put information into the model
print("TextModel1:", TM)
~~~

We provide more detail below, along with tests to make sure your methods are working. 

What methods do we need?
------------------------

First, we recommend starting with these methods:

***Method 1***: `readTextFromFile(self, filename)`: should accept a `filename` (a string) and set `self.text` to all of the text in that file, represented as a single, very large string.


***Method 2***: `makeSentenceLengths(self)`: should use the text in `self.text` to create the `self.sentencelengths` dictionary.
   

***Method 3***: `__repr__(self)`: should generate a string containing all of the dictionaries in the text model, in full---for testing and checking how they are working.
  - This one is provided above... 

There's a good start! Next, implement these:

***Method 4***: `cleanString(self, s)`: should accept a string `s` and return a revised string with no punctuation and no upper-case letters.

***Method 5***: `makeWordLengths(self)`: should use the text in `self.text` to create the `self.wordlengths` dictionary.

***Method 6***: `makeWords(self)`: should use the text in `self.text` to create the `self.words` dictionary

***Method 7***: `makeStems(self)`: should use the text in `self.text` to create the `self.stems` dictionary

***Method 8***: `makeOtherFeature(s)`: should use the text in `self.text` to create the `otherfeature` dictionary. This one is up to you (I used puctuation---feel free to use that or something else...!)

Note that you should choose a better name than `otherfeature`! 

And, the final ones:

***Method 9***: `normalizeDictionary(self, d)`: should accept any single one of the model dictionaries `d` and return a *normalized* version, i.e., one in which the values add up to `1.0`. Remember to *return*, not `print`!

- Use `d.values()` to obtain a list of all of the values of a dictionary `d`.
- In your code, you'll use something like this:
  
`self.normalizedWords = self.normalizedDictionary(self.words)`

- (although you might be able to assign the result to `self.words` itself, depending on how your code works). 

***Method 10***: `smallestValue(self, nd1, nd2)`: should accept any two model dictionaries `nd1` and `nd2` and return the smallest positive (non-zero) value across them both. When used, the two input dictionaries are likely to be normalized, so we've named them `nd1` and `nd2`, but this method should work regardless of whether they're normalized or not. Remember to return, not print!


***Method 11***: `compareDictionaries(self, d, nd1, nd2)`: should compute
- The log-probability that the dictionary `d` arose from the distribution of data in the normalized dictionary `nd1` and.
- The log-probability that dictionary `d` arose from the distribution of data in normalized dictionary `nd`2 and.
- Both of those log-probabilities should be returned in a list, e.g., `[lp1, lp2]`, which stands for log-prob1 and log-prob2.
- Both `nd1` and `nd2` should be normalized first, before computing the log-probabilities.
- `d` does not have to be normalized (in fact, it shouldn't be).
- For any keys in `d` that do not appear in `d1` or `d2`, you should use a value of half the smallest value across both normalized model dictionaries, `d1` and `d2`. Use `smallestValue` to help you here! 

***Method 12***: `compareTextWithTwoModels(self, model1, model2)`: Each of `self`, `model1`, and `model2` should be a `TextModel` with at least five dictionaries. This function should use the `compareDictionaries` method for each of those five dictionaries in self against the corresponding (normalized!) dictionaries in `model1` and `model2`. Then, this method should
- Print out the comparative results of the log-probabilities for all five dictionaries.
- Implement some system for determining which of the two models `self` is closer to, e.g., majority vote from the five dictionaries or weighted sum of the log-probabilities...
- Declare a "winner"---namely the model with which `self` is more similar. 

***Below, there are examples you can try to ensure things are working as they should...***

In addition, this project asks you to use your text-analysis engine! Be sure to:

- Create at least two contrasting text models. These are the "trained" models. You will need to find one or more texts to train each model. If you have multiple texts, you can simply place them all into a single file for processing. For instance, Shakespeare vs. J. K. Rowling was our slides' running example; lots of others are possible! Your two (or more) trained models should use a moderate-or-greater amount of text. (Models based on too small a source text tend to be "brittle"---they depend too much on the idiosyncrasies of that source.)
- Choose at least two other "test texts" that will be compared to your two trained models. Here, you might choose your own writing, or other writing from one or both of your trained models' sources, or something else entirely. The "test" texts or "unknown" texts can be shorter than the trained models and still work well.
 - Run the comparison of your two "test texts" against the two trained models (for a total of at least four comparisons), and write a short paragraph reporting the results, how you obtained them (including how you decided which model would be declared the winner if there were differing underlying dictionary-comparisons), and whether you expected those results...! 

Method-by-method details
------------------------

This section has some method-by-method details on the above pieces of your `TextModel` project.


***`readTextFromFile(self, filename)`***

This method should take in a filename (a string) and should set `self.text` to the text in that file represented as a single, possibly very large string.

Here is an example to try---place this text into a file named `test.txt`:

~~~text
This is a small sentence. This isn't a small sentence, because
this sentence contains more than 10 words and a number! This isn't
a question, is it?
~~~

Then, run these commands at the `python` command prompt:

~~~
TM = TextModel()
# be sure this is in a file named test.txt
test_text = """This is a small sentence. This isn't a small sentence, because
this sentence contains more than 10 words and a number! This isn't
a question, is it?"""

TM.readTextFromFile("test.txt")
print(TM.text == test_text)
~~~

It should print `True`!


***`makeSentenceLengths(self)`***

This method should use the text in `self.text` to create the Python dictionary `self.sentencelengths`.

You'll want to build from the previous assignment's starting point on this---it reuses the way you detected sentence endings in the Markov problem.

Here is a test to check your results:

~~~text
TM = TextModel()
TM.readTextFromFile("test.txt") # Puts all text into TM.text
TM.makeSentenceLengths()        # Uses that text to make lengths
print(TM.sentencelengths)
~~~

which should yield this dictionary:

~~~text
{16: 1, 5: 1, 6: 1}
~~~

because there is one sentence of length 16, one of length 5, and one of length 6.

Note that the key:value pairs in a dictionary may be in any order---yours may differ (this is OK!)


***`cleanString(self, s)`***

This method should accept a string `s` and return a string with no punctuation and no upper-case letters.

- You can use `s = s.lower()` to get rid of upper-case letters.
- Removing punctuation is up to you...
  - One hint: use `import string`
  - And then create a loop such as `for p in string.punctuation`
  - Which will loop the variable `p` over each possible item of `punctuation`...
  - Then you can use `s = s.replace(p, '')` to replace each item of `punctuation` with the empty string!
  - Do try it on a small example first, if you decide to try this path... 
- However, ***don't*** use recursion---use loops (recursion will run out of memory on big strings!) 

Here is a test to check your results:

~~~text
TM = TextModel()
TM.readTextFromFile("test.txt")
clean_s = TM.cleanString(TM.text)
print(clean_s)
~~~

which should yield this string:

~~~text
this is a small sentence this isnt a small sentence because
this sentence contains more than 10 words and a number this isnt
a question is it
~~~

You probably *won't* want to strip numbers away!


***`makeWordLengths(self)`***

This method is similar to `makeSentenceLengths`---except that it makes a dictionary of the word-length features (which are what Sarah Pavis used to identify J. K. Rowling :-))

Be sure to use the ***cleaned*** string for this one---no punctuation!

Here is a test to check your results:

~~~text
TM = TextModel()
TM.readTextFromFile("test.txt")
TM.makeWordLengths()
print(TM.wordlengths)
~~~

which should yield this dictionary:

~~~text
{1: 4, 2: 4, 3: 1, 4: 8, 5: 3, 6: 1, 7: 1, 8: 5}
~~~

Again, the key:value pairs in your dictionary may be in another order---but they should be the same key:value pairs!


***`makeWords(self)`***

This method is similar to `makeWordLengths`---except that it makes a dictionary of words themselves (cleaned!) So, be sure to use the cleaned string for this one, too.

Here is a test to check your results:

~~~text
TM = TextModel()
TM.readTextFromFile("test.txt")
TM.makeWords()
print(TM.words)
~~~

which should yield this dictionary:

~~~text
{'a': 4, '10': 1, 'and': 1, 'because': 1, 'sentence': 3, 'this': 4, 'is': 2, 'contains': 1, 'question': 1,
'number': 1, 'it': 1, 'isnt': 2, 'words': 1, 'small': 2, 'than': 1, 'more': 1}
~~~

As always, the key:value pairs in your dictionary may be in another order---but they should be the same key:value pairs!


***`makeStems(self)`***

This method is similar to `makeWords`---except that it makes a dictionary of the stems of the words themselves (cleaned!) Again, be sure to use the cleaned string for this one, too.

Here is a test to check your results:

~~~text
TM = TextModel()
TM.readTextFromFile("test.txt")
TM.makeStems()
print(TM.stems)
~~~

which, for me, yielded this dictionary:

~~~text
{'a': 4, '10': 1, 'and': 1, 'word': 1, 'sentenc': 3, 'is': 2, 'question': 1, 'becaus': 1, 'number': 1, 'isnt': 2, 'it': 1, 'thi': 4, 'contain': 1, 'small': 2, 'than': 1, 'more': 1}
~~~

Yours may be different, depending on your stemmer! This is totally OK---as long as it is reasonable (not every word has the same stem!), your stemmer is completely OK. (Try adding some different forms of the same words to the file, as well...)

To implement `makeStems`, you will need a function that accepts words and outputs stems. You're invited to:

- Write your own (it should include at least ten stemming rules of the sorts we discussed in class. Don't feel you need to implement all possible rules---in fact, it would be impossible to do so, since there are so many exceptions!
- Or, find a stemming library online and incorporate it into your project.
- Or, use this Porter Stemmer: [PorterStemmerForTextID](https://www.cs.hmc.edu/twiki/bin/view/CS5/PorterStemmerForTextID) , which is one of the original stemming algorithms for English---it's not perfect either, but it is one of the early standards use in the linguistics community.
- To use it, you would place that code into a file named `porter.py` and then include `from porter import create_stem` at the top of your file. From there, call `create_stem(w)`, where `w` is a word whose stem you'd like! 


***`makeOtherFeature(self)`***

This function is similar to `makeWords`, but it's for the feature you choose and create. I named mine `makePunctuation`, but others have used very different features, depending on the texts they're interested in. Do be sure there are at least two items in the dictionary (for texts of a reasonable size)---otherwise it won't be a good feature for comparisons!

Here's my test---please edit, adapt, and adjust it to suit your analysis!

~~~text
TM = TextModel()
TM.readTextFromFile("test.txt")
TM.makePunctuation()
print(TM.punct)
~~~

which, for me, yielded this dictionary:

~~~text
{'!': 1, '?': 1, ',': 2, "'": 2, '.': 1}
~~~

***`__repr__(self)`***

This method should return a representation of all the `TM`'s dictionaries in full, for testing and checking how they are working.

This is provided in the starter code, above.


Testing your `TextModel`'s model-building
---------------------------------------

For the milestone, here is a small set of tests that will check whether your `TextModel` is working. As above, you can:

- Run these from the terminal.
- Or, paste them at the bottom of your file and run them from there---easier! 

Note that you don't need to create a punctuation dictionary! You should, however, create some dictionary other than the basic four: stems, words, word lengths, and sentence lengths. (And, if you like punctuation, it's OK to use it!)

~~~text
# put the text between these triple-quotes into a file named test.txt
test_text = """This is a small sentence. This isn't a small sentence, because
this sentence contains more than 10 words and a number! This isn't
a question, is it?"""

TM = TextModel()
TM.readTextFromFile("test.txt")
assert TM.text == test_text

# Create all of the dictionaries
TM.makeSentenceLengths()
TM.makeWordLengths()
Tm.makeWords()
TM.makeStems()
TM.makePunctuation()

# Let's see all of the dictionaries!
print("The text model has these dictionaries:")
print(TM)
~~~

**Results**

Our results were the following---check that at least the sentence lengths, word lengths, and words are the same!

~~~text
The text model has these dictionaries:
  Words: {'a': 4, '10': 1, 'and': 1, 'because': 1, 'sentence': 3, 'this': 4, 'is': 2, 'contains': 1, 'question': 1, 'number': 1, 'it': 1, 'isnt': 2, 'words': 1, 'small': 2, 'than': 1, 'more': 1}

  Word lengths: {1: 4, 2: 4, 3: 1, 4: 8, 5: 3, 6: 1, 7: 1, 8: 5}

  Stems: {'a': 4, '10': 1, 'and': 1, 'word': 1, 'sentenc': 3, 'is': 2, 'question': 1, 'becaus': 1, 'number': 1, 'isnt': 2, 'it': 1, 'thi': 4, 'contain': 1, 'small': 2, 'than': 1, 'more': 1}

  Sentence lengths: {16: 1, 5: 1, 6: 1}

  Punctuation: {'!': 1, '?': 1, ',': 2, "'": 2, '.': 1}
~~~

Small variations in printing are certainly ok! 


Additional method-by-method details
------------------------------------


These next methods (functions) are more algorithmically challenging, so we describe them in more detail.

***`normalizeDictionary(self, d)`***

This method should accept any single one of the model dictionaries `d` and return a normalized version, i.e., one in which the values add up to `1.0`. Remember to *return*, not print!

Hint: You can use `d.values()` to obtain a list of all of the values of a dictionary, `d`.

Even more important hint: You can loop through all of the keys in a dictionary `d` with

~~~text
    for k in d:
        # do something with the key k and value d[k]
~~~

Here is an example to test your `normalizeDictionary` method:

~~~text
TM = TextModel()
d = {'a': 5, 'b':1, 'c':2}
nd = TM.normalizeDictionary(d)
print("The original dictionary is", d)
print("The normalized dictionary is", nd)

   and here are the output results we obtained:

The original dictionary is {'a': 5, 'c': 2, 'b': 1}
The normalized dictionary is {'a': 0.625, 'c': 0.25, 'b': 0.125}
~~~

***`smallestValue(self, nd1, nd2)`***

This method should accept any two model dictionaries `nd1` and `nd2` and should return the smallest positive (that is, non-zero) value across them both.

When used, the two input dictionaries are likely to be normalized, so we've named them `nd1` and `nd2`, but this method should work regardless of whether they're normalized or not. Remember to return, not print!

Here is an example to test your `smallestValue` method:

~~~text
TM = TextModel()
d1 = {'a': 5, 'b':1, 'c':2}
nd1 = TM.normalizeDictionary(d1)
d2 = {'a': 15, 'd':1}
nd2 = TM.normalizeDictionary(d2)
print("The normalized dictionaries are:")
print(nd1)
print(nd2)
sm_va = TM.smallestValue(nd1, nd2)
print("and the smallest value between them is", sm_va)
~~~
   
and here are the output results we obtained:

~~~text
The normalized dictionaries are:
{'a': 0.625, 'c': 0.25, 'b': 0.125}
{'a': 0.9375, 'd': 0.0625}
and the smallest value between them is 0.0625
~~~

***`compareDictionaries(self, d, nd1, nd2)`***

This method is the fundamental workhorse of the project. The `compareDictionaries` method should compute:

- The log-probability that the dictionary `d` arose from the distribution of data in the normalized dictionary `nd1` and
- The log-probability that dictionary `d` arose from the distribution of data in normalized dictionary `nd2` 

In addition, it should return both of these log-probability values:

- Use `math.log`, which is the natural logarithm (log-base-e).
- Both of those log-probabilities should be returned together in a list, e.g., `[lp1, lp2]` (which stands for log-prob1 and log-prob2, where the first is the probabilities with respect to `nd1` and the second is with respect to `nd2`).
- You should be sure that both `nd1` and `nd2` are normalized first, before computing the log-probabilities.
- On the other hand, `d` does not have to be normalized (in fact, it shouldn't be).
- For any keys in `d` that do not appear in `d1` or `d2`, you should use a value of half the smallest value across both normalized model dictionaries, `d1` and `d2`. Use `smallestValue` to help you here! 


For a detailed example, if you were comparing the unnormalized dictionary `d = {'a':2, 'b':1, 'c':1, 'd':1, 'e':1}` against the normalized dictionary `nd1 = {'a':0.625, 'b':0.125, 'c':0.25}` and the normalized dictionary `nd2 = {'a':0.9375, 'd':0.0625}`, you would compute, first for the comparison with `nd1`,

- Start with a `total_log_prob = 0.0`
- Perhaps define a small value, epsilon, to be half the smallest value in both `nd1` and `nd2` (use the function above...), then use a loop so that:
  - (For the two `'a'`s), you would add `total += 2*math.log(0.625)`
  - (For the one `'b'`), you would add `total += 1*math.log(0.125)`
  - (For the one `'c'`), you would add `total += 1*math.log(0.25)`
  - (For the one `'d'`), you would add `total += 1*math.log(epsilon)`, using that small value (half of it)
  - (For the one `'e'`), you would add `total += 1*math.log(epsilon)`, again using that small value (half of it)
  - Which should yield `-11.337` ... (see below) 

Notes!

- When a key `k` is in `d`, but is is not in `nd1`, be sure to add the probability that is `math.log(epsilon)`
- Behave similarly when `k` is not in `nd2`...
- The same procedure will be used for comparing `d` with `nd2`: you should obtain `-13.29`... 


Here is an example to test your `compareDictionaries` method:

~~~text
TM = TextModel()
d = {'a':2, 'b':1, 'c':1, 'd':1, 'e':1}
print("The unnormalized dictionary is", d)
print("\n")
d1 = {'a': 5, 'b':1, 'c':2}
nd1 = TM.normalizeDictionary(d1)
d2 = {'a': 15, 'd':1}
nd2 = TM.normalizeDictionary(d2)
print("The normalized comparison dictionaries are:")
print(nd1)
print(nd2)

List_of_log_probs = TM.compareDictionaries(d, nd1, nd2)
print("The list of log probs is")
print(List_of_log_probs)
~~~

and here are the output results we obtained:

~~~text
The unnormalized dictionary is {'a': 2, 'c': 1, 'd': 1, 'e': 1, 'b': 1}
The normalized comparison dictionaries are:
{'a': 0.625, 'c': 0.25, 'b': 0.125}
{'a': 0.9375, 'd': 0.0625}
The list of log probs is
[-11.33721496689065, -13.298873472914103]
~~~

(These have been checked by hand, too, so I'm doubly hopeful they're right!)

*A note on interpreting those negative values*

The log-probability is perhaps best thought of as a "shorthand" for very small probabilities. The two values above, about -11.3 and -13.2, mean that:

- The probability of `d` arising from the model `nd1` is `e^-11.3`, and
- The probability of `d` arising from the model `nd2` is `e^-13.2`. 

These numbers are both very small, but the former is more than seven times as likely as the latter.

Put another way, even though the values are negative the *larger probabilities still "win"*---in the sense that they are (often much) more likely.


***`createAllDictionaries(self)`***

This is a small, useful function that simply creates all of the dictionaries with the (raw) input string `self.text`. We provide a version of it for you to use here.

You may need to change it a bit, especially if your fifth feature isn't punctuation!

~~~text
def createAllDictionaries(self):
    """Create out all five of self's
       dictionaries in full.
    """
    self.makeSentenceLengths()
    self.makeWords()
    self.makeStems()
    self.makePunctuation()
    self.makeWordLengths()
~~~

Here are three examples to test this---run these now, since you'll use these three models in the next, final example too!

To test this, create three files:

1. Create a file named `train1.txt` containing this little bit of text:

~~~text
This is a small sentence. This isn't a small sentence, because this
sentence contains more than 10 words and a number!
This isn't a question, is it? 
~~~

2. Create a file named `train2.txt` containing this little bit of text:

~~~text
Many years later, as he faced the firing squad, Colonel Aureliano
Buendia was to remember that distant afternoon when his father
took him to discover ice. 
~~~

3. Create a file named unknown.txt containing this little bit of text:

~~~text
This sentence contains fire and ice! Winter is icy, isn't it? 
~~~

Then, run or paste into the bottom of your `textmodel.py` file (or whatever you've named it!) these example TextModel-building commands:

~~~text
print(" +++++++++++ Model1 +++++++++++ ")
TM1 = TextModel()
TM1.readTextFromFile("train1.txt")
TM1.createAllDictionaries()  # provided in hw description
print(TM1)

print(" +++++++++++ Model2 +++++++++++ ")
TM2 = TextModel()
TM2.readTextFromFile("train2.txt")
TM2.createAllDictionaries()  # provided in hw description
print(TM2)


print(" +++++++++++ Unknown text +++++++++++ ")
TM_Unk = TextModel()
TM_Unk.readTextFromFile("unknown.txt")
TM_Unk.createAllDictionaries()  # provided in hw description
print(TM_Unk)
~~~

and check if your results are similar to these. They don't have to be exact---small differences in implementing stems or sentence-counting or string-cleaning will change the values somewhat:

~~~text
 +++++++++++ Model1 +++++++++++

The text model named [Model1] has dictionaries:

  self.sentencelengths: {16: 1, 5: 1, 6: 1}
  self.words: {'a': 4, '10': 1, 'and': 1, 'because': 1, 'sentence': 3, 'this': 4, 'is': 2, 'contains': 1, 'question': 1, 'number': 1, 'it': 1, 'isnt': 2, 'words': 1, 'small': 2, 'than': 1, 'more': 1}
  self.wordlengths: {1: 4, 2: 4, 3: 1, 4: 8, 5: 3, 6: 1, 7: 1, 8: 5}
  self.stems: {'a': 4, '10': 1, 'and': 1, 'word': 1, 'sentenc': 3, 'is': 2, 'question': 1, 'becaus': 1, 'number': 1, 'isnt': 2, 'it': 1, 'thi': 4, 'contain': 1, 'small': 2, 'than': 1, 'more': 1}
  self.punctuation: {'!': 1, '?': 1, ',': 2, "'": 2, '.': 1}


 +++++++++++ Model2 +++++++++++

The text model named [Model2] has dictionaries:

  self.sentencelengths: {26: 1}
  self.words: {'later': 1, 'father': 1, 'discover': 1, 'years': 1, 'aureliano': 1, 'as': 1, 'buendia': 1, 'distant': 1, 'colonel': 1, 'when': 1, 'ice': 1, 'to': 2, 'squad': 1, 'was': 1, 'his': 1, 'that': 1, 'took': 1, 'him': 1, 'he': 1, 'faced': 1, 'remember': 1, 'many': 1, 'firing': 1, 'afternoon': 1, 'the': 1}
  self.wordlengths: {2: 4, 3: 5, 4: 4, 5: 4, 6: 2, 7: 3, 8: 2, 9: 2}
  self.stems: {'father': 1, 'aureliano': 1, 'as': 1, 'distant': 1, 'year': 1, 'ic': 1, 'colonel': 1, 'when': 1, 'to': 2, 'squad': 1, 'rememb': 1, 'buendia': 1, 'wa': 1, 'that': 1, 'fire': 1, 'took': 1, 'discov': 1, 'hi': 1, 'him': 1, 'he': 1, 'later': 1, 'face': 1, 'afternoon': 1, 'mani': 1, 'the': 1}
  self.punctuation: {',': 2, '.': 1}


 +++++++++++ Unknown text +++++++++++

The text model named [Unknown (trial)] has dictionaries:

  self.sentencelengths: {5: 1, 6: 1}
  self.words: {'and': 1, 'winter': 1, 'sentence': 1, 'this': 1, 'is': 1, 'contains': 1, 'isnt': 1, 'ice': 1, 'it': 1, 'fire': 1, 'icy': 1}
  self.wordlengths: {8: 2, 2: 2, 3: 3, 4: 3, 6: 1}
  self.stems: {'and': 1, 'ici': 1, 'winter': 1, 'fire': 1, 'sentenc': 1, 'is': 1, 'it': 1, 'isnt': 1, 'thi': 1, 'contain': 1, 'ic': 1}
  self.punctuation: {'!': 1, ',': 1, "'": 1, '?': 1}
~~~

Next, you'll compare the `unknown_tm` TextModel with both the `trained_tm1` TextModel and the `trained_tm2` TextModel.


***`compareTextWithTwoModels(self, model1, model2)`***

This method should run the `compareDictionaries` method, described above, for each of the feature dictionaries in `newmodel` against the corresponding (normalized!) dictionaries in `model1` and `model2`. Note that all of those three objects `(self, model1, model2)` will be `TextModel`s.

This method `compareTextWithTwoModels` should:

- Print out the comparative results of the log-probabilities for all five dictionaries---the precise details of how to format and arrange these data are up to you (see below for one example).
- Implement some system for determining which of the two models `self` is closest to, e.g., majority vote from the five dictionaries or weighted sum of the log-probabilities... Again, this part of the algorithm is up to you (below a majority-vote approach is used.).
- Declare a "winner"---namely, it should indicate the model with which `self` is more similar. 

Here, finally, you're welcome to `print` the results, since there are no other functions that will use them downstream! (Though you're welcome to also return things and create additional analysis, if you'd like!)


Here is an example---it uses the three models defined in the previous example:

- `TM1`   (to be used as `model1`)
- `TM2`   (to be used as `model2`)
- `TM_Unk`   (this will be self because it will call `compareTextWithTwoModels`) 

The example compares all five of the dictionaries of `TM_Unk` against the five (normalized!) dictionaries of `TM1` and `TM2`. Admittedly, our examples have far too little text for a real run---but they have the right amount for debugging and making sure things are computing correctly!

Here is the example to try:

~~~text
# the main comparison method
TM_Unk.compareTextWithTwoModels(TM1, TM2)
~~~

and here are our results---your formatting, overall model-choosing, and some other details may certainly be different:

~~~text
Overall comparison:

                name       vsTM1      vsTM2
                ----       -----      -----
               words      -35.16     -43.15
         wordlengths      -24.02     -22.00
     sentencelengths       -2.20      -3.58
               stems      -35.16     -42.42
         punctuation       -6.40      -8.32


  -->  Model1 wins on 4 features
  -->  Model2 wins on 1 features

  +++++      Model1 is the better match!      +++++
~~~

Your own texts and analysis
---------------------------

Finally, this project asks you to use your text-analysis engine! Be sure to:

 1. Create at least two contrasting text models. These are the "trained" models. You will need to find one or more texts to train each model. If you have multiple texts from the same author, you can simply place them all into a single file for processing. For instance, Shakespeare vs. J. K. Rowling was our slides' running example; lots of others are possible! Your two (or more) trained models should use a moderate-or-greater amount of text. (Models based on too small a source text tend to be "brittle"---they depend too much on the idiosyncrasies of that source.)
 2. Choose at least two other "test texts" that will be compared to your two trained models. Here, you might choose your own writing, or other writing from one or both of your trained models' sources, or something else entirely. The "test" texts or "unknown" texts can be shorter than the trained models and still work well.
 3. Run the comparison of your two "test texts" against the two trained models (for a total of at least four comparisons).
 
If you try to open a file and get an error similar to this: `codec can't encode character ... in ... position`,
try using different encodings in your `readTextFromFile` method, e.g.,

- `open(filename, encoding = 'latin1')` or
- `open(filename, encoding = 'utf-8')`

Extras are encouraged:

- Using more trained models or more test texts.
- Using more features or features carefully tuned to the texts you're investigating.
- Other creative extras that are specific to your particular analysis... 
