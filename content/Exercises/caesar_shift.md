---
title: "Caesar Shift"
date: 2018-06-28T09:47:47-04:00
draft: false
weight: 1550
---

Background
----------
The Caesar Shift is one of the simplest and most widely known encryption techniques. It is a type of substitution cipher in which each letter in the plaintext (that is, the text to be encrypted) is replaced by a letter some fixed number of positions down the alphabet. For example, with a shift of 3, A would be replaced by D, B would become E, and so on. We will be implementing functions to encrypt and decrypt text using this cipher!

***Part 1***: `encipher(S, n)`

Write the function `encipher(S , n)` whose first argument `S` is a string and whose second argument `n` is a non-negative integer between 0 and 25. Then, `encipher` should return a new string in which the letters in `S` have been "rotated" by `n` characters forward in the alphabet, wrapping around as needed.

For this problem, you should assume that upper-case letters are "rotated" to upper-case letters, lower-case letters are "rotated" to lower-case letters, and all non-alphabetic characters are left unchanged. For example, if we were to shift the letter 'y' by 3, we would get 'b' and if we were to shift the letter 'Y' by 3 we would get 'B'. (In `python`, you can use the test `if 'a' <= c and c <= 'z':` to determine if a character `c` is between 'a' and 'z' in the alphabet.)

You can write `encipher` any way you like as long as you use functional programming---that is, feel free to use any combination of conditionals, recursion, and list comprehensions.

You might use the class suggestion of writing a helper function that "rotates" a single character by `n` spots, wrapping around the alphabet as appropriate. In lecture we looked at how that might work. Then, you could use this helper function to `encipher` your string. It's up to you how you do this!

That said, for rotating, keep in mind that the built-in functions `ord` and `chr` convert from single-character strings to integers and back:

For example, `ord('a')` returns `97` and `chr(97)` returns `'a'`. 

Remember that

- Uppercase letters wrap around the alphabet to uppercase letters.
- Lowercase letters wrap always to lowercase letters.
- Non-letters do not wrap or change at all!

{{% notice tip %}}
You can start by writing a function `rot(c, n)` that rotates `c`, a single character, forward by `n` spots in the alphabet.
We wrote `rot13(c)` in class---it's very close to `rot(c, n)`!
Remember that you'll need to wrap the alphabet (as `rot13` did) and leave non-alphabetic characters unchanged
{{% /notice %}}

Test out your `rot(c, n)` function to make sure it works:
~~~text
assert rot('a', 2)  ==  'c'
assert rot('y', 2)  ==  'a' 
assert rot('A', 3)  ==  'D'
assert rot('Y', 3)  ==  'B'
assert rot(' ', 4)  ==  ' '
~~~

{{% notice tip %}} 
If you have `rot(c, n)`, you're nearly there!
With `rot(c, n)`, this problem is identical to the dna_to_rna (`transcribe`) problem!
That is, you can handle one letter at a time---recursively---using `rot(c, n)`, with a base case (an empty-string `S`)...
Alternatively, you can use a list comprehension to apply `rot(c, n)` many times.
If you do use a list comprehension, then use `list_to_str` (below) to get back to a string!
{{% /notice %}}

~~~text
def list_to_str(L):
    """L must be a list of characters;
       this function returns a single string made from them.
    """
    if len(L) == 0:
        return ''
    return L[0] + list_to_str(L[1:])

assert list_to_str(['v', 'a', 's', 's', 'a', 'r', '!']) == 'vassar!'
~~~

However you implement `encipher`, be sure to test! Here's a start:
~~~text
assert encipher('xyza', 1) == 'yzab'
assert encipher('Z A', 1) == 'A B'
~~~

Here are some more examples; we encourage you to turn them into asserts:
~~~text
>>> encipher('xyza', 1)
'yzab'

>>> encipher('Z A', 1)
'A B'

>>> encipher('*ab?', 1)
'*bc?'

>>> encipher('This is a string!', 1)
'Uijt jt b tusjoh!'

>>> encipher('Caesar cipher? I prefer Caesar salad.', 25)
'Bzdrzq bhogdq? H oqdedq Bzdrzq rzkzc.'
~~~


***Part 2***: `decipher(S)`

On the other hand, `decipher(S)` will be given a string of English text already shifted by some amount. Then, `decipher` should return, to the best of its ability, the original English string, which will be some rotation (possibly 0) of the argument `S`.

Note: some strings have more than one English "deciphering." What's more, it is difficult or impossible to handle very short strings correctly. Thus, your decipher function does not have to be perfect. However, it should work almost all of the time on long stretches of English text, e.g., sentences of 8+ words. On a single word or short phrase, you will not lose any credit for not getting the correct deciphering!

A good place to start is to create a line with every possible ENCODING, something like this:
~~~text
L = [    __________        for n in range(26) ]
~~~

Then, you will want to use the LoL "list of lists" technique in which each element of `L` gets a score. You might want to look back at how that worked...
~~~text
LoL = [    __________        for x in L ]
~~~

It's entirely up to you how you might want to score "Englishness." See below for some starting points... .
You can go back and take a look at the min/max lecture to see how to handle the LoL "list of lists" 

One way to rate the Englishness of a string is to look at the percentage of vowels in the string---English should have more vowels in it than random strings! You could use this fact to rate which sentences are more likely to be English, and then pick the most likely one to be the deciphered string!

You are welcome to implement additional methods for guessing what string is correct, but only if you would like to! Another approach you could try is to use letter frequencies---a function providing those frequencies is provided below. Feel free to cut-and-paste it into your file. Scrabble scores have also been suggested in the past! You're welcome to use some additional "heuristics" (rules of thumb) of your own design. Also, you are welcome to write one or more small "helper" functions that will assist in writing decipher.


Some decipher examples:
~~~text
>>> decipher('Bzdrzq bhogdq? H oqdedq Bzdrzq rzkzc.')
'Caesar cipher? I prefer Caesar salad.'

>>> decipher('Hu lkbjhapvu pz doha ylthpuz hmaly dl mvynla '\
              'lclyfaopun dl ohcl slhyulk.')
'An education is what remains after we forget everything we have learned.'

>>> decipher('Onyx balks')
'Edon rqbai'  # mine is wrong! This is OK here...
~~~

Again, we encourage you to turn these examples (at least the first two!) into asserts.

Note that the last example shows that our decipherer gets some short phrases wrong---this is completely OK!. As phrases get longer, your decipherer should get more and more of them correct, but it does not have to get single words or short phrases---after all, for short strings, there are likely to be rotations that have more "English-y" letters than the original! 


~~~text
# table of probabilities for each letter...
def let_prob(c):
    """If c is the space character or an alphabetic character,
       we return its monogram probability (for english),
       otherwise we return 1.0.  We ignore capitalization.
       Adapted from
       http://www.cs.chalmers.se/Cs/Grundutb/Kurser/krypto/en_stat.html
    """
    if c == ' ': return 0.1904
    if c == 'e' or c == 'E': return 0.1017
    if c == 't' or c == 'T': return 0.0737
    if c == 'a' or c == 'A': return 0.0661
    if c == 'o' or c == 'O': return 0.0610
    if c == 'i' or c == 'I': return 0.0562
    if c == 'n' or c == 'N': return 0.0557
    if c == 'h' or c == 'H': return 0.0542
    if c == 's' or c == 'S': return 0.0508
    if c == 'r' or c == 'R': return 0.0458
    if c == 'd' or c == 'D': return 0.0369
    if c == 'l' or c == 'L': return 0.0325
    if c == 'u' or c == 'U': return 0.0228
    if c == 'm' or c == 'M': return 0.0205
    if c == 'c' or c == 'C': return 0.0192
    if c == 'w' or c == 'W': return 0.0190
    if c == 'f' or c == 'F': return 0.0175
    if c == 'y' or c == 'Y': return 0.0165
    if c == 'g' or c == 'G': return 0.0161
    if c == 'p' or c == 'P': return 0.0131
    if c == 'b' or c == 'B': return 0.0115
    if c == 'v' or c == 'V': return 0.0088
    if c == 'k' or c == 'K': return 0.0066
    if c == 'x' or c == 'X': return 0.0014
    if c == 'j' or c == 'J': return 0.0008
    if c == 'q' or c == 'Q': return 0.0008
    if c == 'z' or c == 'Z': return 0.0005
    return 1.0
~~~
