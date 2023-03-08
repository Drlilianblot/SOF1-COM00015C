# A deeper dive into Strings, Lists and Tuples



## String traversal with a `for` loop

A lot of computations involve processing a string one character at a time. Often they start at the beginning, select each character in turn, do something to it, and continue until the end. This pattern of processing is called a **traversal**. One way to write a traversal is with a `while` loop:

{% code lineNumbers="true" %}
```python
fruit = 'banana'
index = 0 
while index < len(fruit): 
     letter = fruit[index] 
     print(letter) 
     index = index + 1 
```
{% endcode %}

This loop traverses the string and displays each letter on a line by itself. The loop condition is `index < len(fruit)`, so when `index` is equal to the length of the string, the condition is false, and the body of the loop is not executed. The last character accessed is the one with the index `len(fruit)-1`, which is the last character in the string.

**Exercise:** Write a function that takes a string as an argument and displays the letters backward, one per line.

<details>

<summary>answer:</summary>



</details>

Another way to write a traversal is with a `for` loop:

{% code lineNumbers="true" %}
```
for char in fruit: 
    print(char) 
```
{% endcode %}

Each time through the loop, the next character in the string is assigned to the variable `char`. The loop continues until no characters are left.

The following example shows how to use concatenation (string addition) and a `for` loop to generate an abecedarian series (that is, in alphabetical order). In Robert McCloskey's book  "_Make Way for Ducklings_", the names of the ducklings are Jack, Kack, Lack, Mack, Nack, Ouack, Pack, and Quack. This loop outputs these names in order:

{% code lineNumbers="true" %}
```python
prefixes = 'JKLMNOPQ' 
suffix = 'ack'
for letter in prefixes: 
    print(letter + suffix) 
```
{% endcode %}

The output is:

```
Jack 
Kack 
Lack 
Mack 
Nack 
Oack 
Pack 
Qack 
```

Of course, that's not quite right because "Ouack" and "Quack" are misspelled.

**Exercise:** Modify the program to fix this error.&#x20;

<details>

<summary>Answer:</summary>



</details>



## Searching

What does the following function do?

{% code lineNumbers="true" %}
```python
def find(word, letter): 
    index = 0 
    while index < len(word): 
        if word[index] == letter: 
            return index 
        index = index + 1 
    return -1 
```
{% endcode %}

In a sense, `find` is the opposite of the `[ ]` operator. Instead of taking an index and extracting the corresponding character, it takes a character and finds the index where that character appears. If the character is not found, the function returns `-1`. This is the first example we have seen of a `return` statement inside a loop. If `word[index] == letter`, the function breaks out of the loop and returns immediately. If the character doesn't appear in the string, the program exits the loop normally and returns `-1`. This pattern of computation - traversing a sequence and returning when we find what we are looking for - is called a **search**.

**Exercise:** Modify `find` so that it has a third parameter, the index in `word` where it should start looking.&#x20;

<details>

<summary>answer:</summary>



</details>

## Looping and counting

The following program counts the number of times the letter `a` appears in a string:

{% code lineNumbers="true" %}
```python
word = 'banana' 
count = 0 
for letter in word: 
    if letter == 'a': 
        count = count + 1 
print(count) 
```
{% endcode %}

This program demonstrates another pattern of computation called a **counter**. The variable `count` is initialized to `0` and then incremented each time an `a` is found. When the loop exits, `count` contains the result - the total number of `a`'s.

**Exercise:** Encapsulate this code in a function named `count`, and generalise it so that it accepts the string and the letter as arguments.&#x20;

<details>

<summary>Answer:</summary>



</details>

**Exercise:** Rewrite this function so that instead of traversing the string from the beginning, it uses the three-parameter version of `find` from the previous section.

<details>

<summary>Answer:</summary>



</details>

## `String` methods

A `method` is similar to a function - it takes arguments and may return a value - but the syntax is different. For example, the method `upper` takes a string and returns a new string with all uppercase letters;  Instead of the function syntax `upper(word)`, it uses the method syntax `word.upper()`. This is known as the **dot** notation.

<pre class="language-bash"><code class="lang-bash">>>> word = 'banana'
<strong>>>> new_word = word.upper() 
</strong>>>> print(new_word)
 BANANA 
</code></pre>

This form of dot notation specifies the name of the method, `upper`, and the name of the string to apply the method to, `word`. The empty parentheses indicate that this method takes no argument.

A method call is called an **invocation**; in this case, we would say that we are invoking `upper` on the `word`. As it turns out, there is a string method named `find` that is remarkably similar to the function we wrote:

```bash
>>> word = 'banana' 
>>> index = word.find('a') 
>>> print(index) 
 1 
```

In this example, we invoke find} on {\tt word} and pass the letter we are looking for as a parameter. % Actually, the {\tt find} method is more general than our function; it can find substrings, not just characters:

\beforeverb \begin{pyinterpreter}

> > > word.find('na') 2 \end{pyinterpreter} \afterverb % It can take as a second argument the index where it should start:

\index{optional argument} \index{argument!optional}

\beforeverb \begin{pyinterpreter}

> > > word.find('na', 3) 4 \end{pyinterpreter} \afterverb % And as a third argument the index where it should stop:

\beforeverb \begin{pyinterpreter}

> > > name = 'bob' name.find('b', 1, 2) -1 \end{pyinterpreter} \afterverb % This search fails because {\tt b} does not appear in the index range from {\tt 1} to {\tt 2} (not including {\tt 2}).

\begin{exercise} \index{count method} \index{method!count}

There is a string method called {\tt count} that is similar to the function in the previous exercise. Read the documentation of this method and write an invocation that counts the number of {\tt a} in \verb"'banana'". \end{exercise}

\section{The {\tt in} operator} \label{sec:in-both}

\index{in operator} \index{operator!in} \index{boolean operator} \index{operator!boolean}

The word {\tt in} is a boolean operator that takes two strings and returns {\tt True} if the first appears as a substring in the second:

\beforeverb \begin{pyinterpreter}

> > > 'ana' in 'banana' True 'rama' in 'banana' False \end{pyinterpreter} \afterverb %

\newpage

For example, the following function prints all the letters from {\tt word1} that also appear in {\tt word2}:

\beforeverb \begin{pycode} def in\_both(word1, word2): for letter in word1: if letter in word2: print(letter) \end{pycode} \afterverb % With well-chosen variable names, Python sometimes reads like English. You could read this loop, \`\`for (each) letter in (the first) word, if (the) letter (appears) in (the second) word, print (the) letter.''

Here's what you get if you compare apples and oranges:

\beforeverb \begin{pyinterpreter}

> > > in\_both('apples', 'oranges') a e s \end{pyinterpreter} \afterverb %

\section{String comparison}

\index{string!comparison} \index{comparison!string}

The relational operators work on strings. To see if two strings are equal:

\beforeverb \begin{pycode} if word == 'banana': print ('All right, bananas.') \end{pycode} \afterverb % Other relational operations are useful for putting words in alphabetical order:

\beforeverb \begin{pycode} if word < 'banana': print('Your word,' + word + ', comes before banana.') elif word > 'banana': print('Your word,' + word + ', comes after banana.') else: print('All right, bananas.') \end{pycode} \afterverb % %Python does not handle uppercase and lowercase letters the same way %that people do. All the uppercase letters come before all the %lowercase letters, so: % %\beforeverb %\begin{pycode} %Your word, Pineapple, comes before banana. %\end{pycode} %\afterverb %% %A common way to address this problem is to convert strings to a %standard format, such as all lowercase, before performing the %comparison. Keep that in mind in case you have to defend yourself %against a man armed with a Pineapple.

\newpage

\section{Debugging} \index{debugging}

\index{traversal}

When you use indices to traverse the values in a sequence, it is tricky to get the beginning and end of the traversal right. Here is a function that is supposed to compare two words and return {\tt True} if one of the words is the reverse of the other, but it contains two errors:

\beforeverb \begin{pycode} def is\_reverse(word1, word2): if len(word1) != len(word2): return False

```
i = 0
j = len(word2)

while j > 0:
    if word1[i] != word2[j]:
        return False
    i = i+1
    j = j-1

return True
```

\end{pycode} \afterverb % The first {\tt if} statement checks whether the words are the same length. If not, we can return {\tt False} immediately and then, for the rest of the function, we can assume that the words are the same length. This is an example of the guardian pattern in \prettyref{sec:guardian}. % \index{guardian pattern} \index{pattern!guardian} \index{index} % {\tt i} and {\tt j} are indices: {\tt i} traverses {\tt word1} forward while {\tt j} traverses {\tt word2} backward. If we find two letters that don't match, we can return {\tt False} immediately. If we get through the whole loop and all the letters match, we return {\tt True}.

If we test this function with the words `pots'' and` stop'', we expect the return value {\tt True}, but we get an IndexError:

\index{IndexError} \index{exception!IndexError}

\beforeverb \begin{pyinterpreter}

> > > is\_reverse('pots', 'stop') ... File "reverse.py", line 15, in is\_reverse if word1\[i] != word2\[j]: IndexError: string index out of range \end{pyinterpreter} \afterverb % For debugging this kind of error, my first move is to print the values of the indices immediately before the line where the error appears.

\beforeverb \begin{pycode} while j > 0: print(i, j) # print here

```
    if word1[i] != word2[j]:
        return False
    i = i+1
    j = j-1
```

\end{pycode} \afterverb % Now when I run the program again, I get more information:

\beforeverb \begin{pyinterpreter}

> > > is\_reverse('pots', 'stop') 0 4 ... IndexError: string index out of range \end{pyinterpreter} \afterverb % The first time through the loop, the value of {\tt j} is 4, which is out of range for the string \verb"'pots'". The index of the last character is 3, so the initial value for {\tt j} should be {\tt len(word2)-1}.

\index{semantic error} \index{error!semantic}

If I fix that error and run the program again, I get:

\beforeverb \begin{pyinterpreter}

> > > is\_reverse('pots', 'stop') 0 3 1 2 2 1 True \end{pyinterpreter} \afterverb % This time we get the right answer, but it looks like the loop only ran three times, which is suspicious. To get a better idea of what is happening, it is useful to draw a state diagram. During the first iteration, the frame for \verb"is\_reverse" looks like this:

\index{state diagram} \index{diagram!state}

\beforefig \centerline{\includegraphics{figs/state4.eps\}} \afterfig

I took a little license by arranging the variables in the frame and adding dotted lines to show that the values of {\tt i} and {\tt j} indicate characters in {\tt word1} and {\tt word2}.

\begin{exercise} \label{exo:is-reverse} Starting with this diagram, execute the program on paper, changing the values of {\tt i} and {\tt j} during each iteration. Find and fix the second error in this function. \end{exercise}

\section{Glossary}

\begin{vocabulary}\[object:] Something a variable can refer to. For now, you can use `object'' and` value'' interchangeably. \index{object} \end{vocabulary}

\begin{vocabulary}\[sequence:] An ordered set; that is, a set of values where each value is identified by an integer index. \index{sequence} \end{vocabulary}

\begin{vocabulary}\[item:] One of the values in a sequence. \index{item} \end{vocabulary}

\begin{vocabulary}\[index:] An integer value used to select an item in a sequence, such as a character in a string. \index{index} \end{vocabulary}

\begin{vocabulary}\[slice:] A part of a string specified by a range of indices. \index{slice} \end{vocabulary}

\begin{vocabulary}\[empty string:] A string with no characters and length 0, represented by two quotation marks. \index{empty string} \end{vocabulary}

\begin{vocabulary}\[immutable:] The property of a sequence whose items cannot be assigned. \index{immutability} \end{vocabulary}

\begin{vocabulary}\[traverse:] To iterate through the items in a sequence, performing a similar operation on each. \index{traversal} \end{vocabulary}

\begin{vocabulary}\[search:] A pattern of traversal that stops when it finds what it is looking for. \index{search pattern} \index{pattern!search} \end{vocabulary}

\begin{vocabulary}\[counter:] A variable used to count something, usually initialized to zero and then incremented. \index{counter} \end{vocabulary}

\begin{vocabulary}\[method:] A function that is associated with an object and called using dot notation. \index{method} \end{vocabulary}

\begin{vocabulary}\[invocation:] A statement that calls a method. \index{invocation} \end{vocabulary}

\section{Exercises}

\begin{exercise}

\index{step size} \index{slice operator} \index{operator!slice}

A string slice can take a third index that specifies the \`\`step size;'' that is, the number of spaces between successive characters. A step size of 2 means every other character; 3 means every third, etc.

\beforeverb \begin{pyexo}

> > > fruit = 'banana' fruit\[0:5:2] 'bnn' \end{pyexo} \afterverb

A step size of -1 goes through the word backwards, so the slice \verb"\[::-1]" generates a reversed string. % \index{palindrome} % Use this idiom to write a one-line version of \verb"is\_palindrome" from \prettyref{exo:palindrome}. \end{exercise}

\begin{exercise} \index{letter rotation} \index{rotation, letter}

\label{exo:rotate} ROT13 is a weak form of encryption that involves \`\`rotating'' each letter in a word by 13 places\footnote{See \url{wikipedia.org/wiki/ROT13}.}. To rotate a letter means to shift it through the alphabet, wrapping around to the beginning if necessary, so 'A' shifted by 3 is 'D' and 'Z' shifted by 1 is 'A'.

Write a function called \verb"rotate\_word" that takes a string and an integer as parameters, and that returns a new string that contains the letters from the original string \`\`rotated'' by the given amount.

For example, `cheer'' rotated by 7 is` jolly'' and `melon'' rotated by -10 is` cubed''.\
% %%For example `sleep'' %%rotated by 9 is` bunny'' and `latex'' rotated by 7 is` shale''. % You might want to use the built-in functions {\tt ord}, which converts a character to a numeric code, and {\tt chr}, which converts numeric codes to characters. % %Potentially offensive jokes on the Internet are sometimes encoded %in ROT13. If you are not easily offended, find and decode some %of them. \end{exercise}

\newpage

\begin{exercise} \index{string method} \index{method!string}

Read the documentation of the string methods at \url{docs.python.org/lib/string-methods.html}. You might want to experiment with some of them to make sure you understand how they work. {\tt strip} and {\tt replace} are particularly useful. % The documentation uses a syntax that might be confusing. For example, in \verb"find(sub\[, start\[, end]])", the brackets indicate optional arguments. So {\tt sub} is required, but {\tt start} is optional, and if you include {\tt start}, then {\tt end} is optional. \end{exercise}

\begin{exercise} The following functions are all {\em intended} to check whether a string contains any lowercase letters, but at least some of them are wrong. For each function, describe what the function actually does (assuming that the parameter is a string).

\begin{pyexo} def any\_lowercase1(s): for c in s: if c.islower(): return True else: return False \end{pyexo}

%\begin{pyexo} %def any\_lowercase2(s): % for c in s: % if 'c'.islower(): % return 'True' % else: % return 'False' %\end{pyexo}

\begin{pyexo} def any\_lowercase3(s): for c in s: flag = c.islower() return flag \end{pyexo}

\begin{pyexo} def any\_lowercase4(s): flag = False for c in s: flag = flag or c.islower() return flag \end{pyexo}

\begin{pyexo} def any\_lowercase5(s): for c in s: if not c.islower(): return False return True \end{pyexo}

\end{exercise}
