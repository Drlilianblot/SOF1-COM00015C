# Lists

% \chapterimage{chapter\_head\_1.pdf} \chapter{Lists} \label{cha:lists}

\index{list} \index{type!list}

The `in` operator also works on lists.

\beforeverb \begin{pycode}

> > > cheeses = \['Cheddar', 'Edam', 'Gouda'] 'Edam' in cheeses True 'Brie' in cheeses False \end{pycode} \afterverb

\section{Traversing a list} \index{list!traversal} \index{traversal!list} \index{for loop} \index{loop!for} \index{statement!for}

The most common way to traverse the elements of a list is with a {\tt for} loop. The syntax is the same as for strings:

\beforeverb \begin{pycode} for cheese in cheeses: print(cheese) \end{pycode} \afterverb % This works well if you only need to read the elements of the list. But if you want to write or update the elements, you need the indices. A common way to do that is to combine the functions {\tt range} and {\tt len}:

\index{looping!with indices} \index{index!looping with}

\beforeverb \begin{pycode} for i in range(len(numbers)): numbers\[i] = numbers\[i] \* 2 \end{pycode} \afterverb % This loop traverses the list and updates each element. {\tt len} returns the number of elements in the list. {\tt range} returns a list of indices from 0 to $n-1$, where $n$ is the length of the list. Each time through the loop {\tt i} gets the index of the next element. The assignment statement in the body uses {\tt i} to read the old value of the element and to assign the new value.

\index{item update} \index{update!item}

A {\tt for} loop over an empty list never executes the body:

\beforeverb \begin{pycode} for x in \[]: print('This never happens.') \end{pycode} \afterverb % Although a list can contain another list, the nested list still counts as a single element. The length of this list is four:

\index{nested list} \index{list!nested}

\beforeverb \begin{pyoutput} \['spam', 1, \['Brie', 'Roquefort', 'Pol le Veq'], \[1, 2, 3]] \end{pyoutput} \afterverb

\newpage

\section{List operations} \index{list!operation}

The {\tt +} operator concatenates lists:

\index{concatenation!list} \index{list!concatenation}

\beforeverb \begin{pycode}

> > > a = \[1, 2, 3] b = \[4, 5, 6] c = a + b print(c) \[1, 2, 3, 4, 5, 6] \end{pycode} \afterverb % Similarly, the {\tt \*} operator repeats a list a given number of times:

\index{repetition!list} \index{list!repetition}

\beforeverb \begin{pycode}

> > > \[0] \* 4 \[0, 0, 0, 0] \[1, 2, 3] \* 3 \[1, 2, 3, 1, 2, 3, 1, 2, 3] \end{pycode} \afterverb % The first example repeats {\tt \[0]} four times. The second example repeats the list {\tt \[1, 2, 3]} three times.

\section{List slices}

\index{slice operator} \index{operator!slice} \index{index!slice} \index{list!slice} \index{slice!list}

The slice operator also works on lists:

\beforeverb \begin{pycode}

> > > t = \['a', 'b', 'c', 'd', 'e', 'f'] t\[1:3] \['b', 'c'] t\[:4] \['a', 'b', 'c', 'd'] t\[3:] \['d', 'e', 'f'] \end{pycode} \afterverb % If you omit the first index, the slice starts at the beginning. If you omit the second, the slice goes to the end. So if you omit both, the slice is a copy of the whole list.

\index{list!copy} \index{slice!copy} \index{copy!slice}

\beforeverb \begin{pycode}

> > > t\[:] \['a', 'b', 'c', 'd', 'e', 'f'] \end{pycode} \afterverb % Since lists are mutable, it is often useful to make a copy before performing operations that fold, spindle or mutilate lists.

\index{mutability}

\newpage

A slice operator on the left side of an assignment can update multiple elements:

\index{slice!update} \index{update!slice}

\beforeverb \begin{pycode}

> > > t = \['a', 'b', 'c', 'd', 'e', 'f'] t\[1:3] = \['x', 'y'] print(t) \['a', 'x', 'y', 'd', 'e', 'f'] \end{pycode} \afterverb %

% You can add elements to a list by squeezing them into an empty % slice:

% \beforeverb % \begin{pycode} % >>> t = \['a', 'd', 'e', 'f'] % >>> t\[1:1] = \['b', 'c'] % >>> print t % \['a', 'b', 'c', 'd', 'e', 'f'] % \end{pycode} % \afterverb % % And you can remove elements from a list by assigning the empty list to % them:

% \beforeverb % \begin{pycode} % >>> t = \['a', 'b', 'c', 'd', 'e', 'f'] % >>> t\[1:3] = \[] % >>> print t % \['a', 'd', 'e', 'f'] % \end{pycode} % \afterverb % % But both of those operations can be expressed more clearly % with list methods.

\section{List methods}

\index{list!method} \index{method, list}

Python provides methods that operate on lists. For example, {\tt append} adds a new element to the end of a list:

\index{append method} \index{method!append}

\beforeverb \begin{pycode}

> > > t = \['a', 'b', 'c'] t.append('d') print(t) \['a', 'b', 'c', 'd'] \end{pycode} \afterverb % {\tt extend} takes a list as an argument and appends all of the elements:

\index{extend method} \index{method!extend}

\beforeverb \begin{pycode}

> > > t1 = \['a', 'b', 'c'] t2 = \['d', 'e'] t1.extend(t2) print(t1) \['a', 'b', 'c', 'd', 'e'] \end{pycode} \afterverb % This example leaves {\tt t2} unmodified.

{\tt sort} arranges the elements of the list from low to high:

\index{sort method} \index{method!sort}

\beforeverb \begin{pycode}

> > > t = \['d', 'c', 'e', 'b', 'a'] t.sort() print(t) \['a', 'b', 'c', 'd', 'e'] \end{pycode} \afterverb % List methods are all void; they modify the list and return {\tt None}. If you accidentally write {\tt t = t.sort()}, you will be disappointed with the result.

\index{void method} \index{method!void} \index{None special value} \index{special value!None}

\newpage

\section{Map, filter and reduce}

To add up all the numbers in a list, you can use a loop like this:

% see add.py

\beforeverb \begin{pycode} def add\_all(a\_list): total = 0 for val in a\_list: total += val return total \end{pycode} \afterverb % {\tt total} is initialized to 0. Each time through the loop, {\tt x} gets one element from the list. The {\tt +=} operator provides a short way to update a variable. This {\bf augmented assignment statement}:

\index{update operator} \index{operator!update}

\index{assignment!augmented} \index{augmented assignment}

\beforeverb \begin{pycode} total += val \end{pycode} \afterverb % is equivalent to:

\beforeverb \begin{pycode} total = total + val \end{pycode} \afterverb % As the loop executes, {\tt total} accumulates the sum of the elements; a variable used this way is sometimes called an {\bf accumulator}. % \index{accumulator!sum} % Adding up the elements of a list is such a common operation that Python provides it as a built-in function, {\tt sum}:

\beforeverb \begin{pycode}

> > > t = \[1, 2, 3] sum(t) 6 \end{pycode} \afterverb % An operation like this that combines a sequence of elements into a single value is sometimes called {\bf reduce}.

\index{reduce pattern} \index{pattern!reduce} \index{traversal}

Sometimes you want to traverse one list while building another. For example, the following function takes a list of strings and returns a new list that contains capitalized strings:

\beforeverb \begin{pycode} def capitalize\_all(word): result = \[] for letter in word: result.append(letter.capitalize()) return result \end{pycode} \afterverb % {\tt result} is initialized with an empty list; each time through the loop, we append the next element. So {\tt result} is another kind of accumulator. % \index{accumulator!list} % An operation like \verb"capitalize\_all" is sometimes called a {\bf map} because it \`\`maps'' a function (in this case the method {\tt capitalize}) onto each of the elements in a sequence.

\index{map pattern} \index{pattern!map} \index{filter pattern} \index{pattern!filter}

\newpage

Another common operation is to select some of the elements from a list and return a sublist. For example, the following function takes a list of strings and returns a list that contains only the uppercase strings:

\beforeverb \begin{pycode} def only\_upper(word): result = \[] for letter in word: if letter.isupper(): result.append(letter) return result \end{pycode} \afterverb % {\tt isupper} is a string method that returns {\tt True} if the string contains only upper case letters. % An operation like \verb"only\_upper" is called a {\bf filter} because it selects some of the elements and filters out the others.

Most common list operations can be expressed as a combination of map, filter and reduce. Because these operations are so common, Python provides language features to support them, including the built-in function {\tt map} and an operator called a \`\`list comprehension.''

\index{list!comprehension}

\begin{exercise} \label{exo:cumulative} \index{cumulative sum}

Write a function that takes a list of numbers and returns the cumulative sum; that is, a new list where the $i$th element is the sum of the first $i+1$ elements from the original list. For example, the cumulative sum of {\tt \[1, 2, 3]} is {\tt \[1, 3, 6]}. \end{exercise}

\section{Deleting elements}

\index{element deletion} \index{deletion, element of list}

There are several ways to delete elements from a list. If you know the index of the element you want, you can use {\tt pop}:

\index{pop method} \index{method!pop}

\beforeverb \begin{pycode}

> > > t = \['a', 'b', 'c'] x = t.pop(1) print(t) \['a', 'c'] print(x) b \end{pycode} \afterverb % {\tt pop} modifies the list and returns the element that was removed. If you don't provide an index, it deletes and returns the last element.

If you don't need the removed value, you can use the {\tt del} operator:

\index{del operator} \index{operator!del}

\beforeverb \begin{pycode}

> > > t = \['a', 'b', 'c'] del t\[1] print(t) \['a', 'c'] \end{pycode} \afterverb %

If you know the element you want to remove (but not the index), you can use {\tt remove}:

\index{remove method} \index{method!remove}

\beforeverb \begin{pycode}

> > > t = \['a', 'b', 'c'] t.remove('b') print(t) \['a', 'c'] \end{pycode} \afterverb % The return value from {\tt remove} is {\tt None}.

\index{None special value} \index{special value!None}

To remove more than one element, you can use {\tt del} with a slice index:

\beforeverb \begin{pycode}

> > > t = \['a', 'b', 'c', 'd', 'e', 'f'] del t\[1:5] print(t) \['a', 'f'] \end{pycode} \afterverb % As usual, the slice selects all the elements up to, but not including, the second index.

\section{Lists and strings}

\index{list} \index{string} \index{sequence}

A string is a sequence of characters and a list is a sequence of values, but a list of characters is not the same as a string. To convert from a string to a list of characters, you can use {\tt list}:

\index{list!function} \index{function!list}

\beforeverb \begin{pycode}

> > > s = 'spam' t = list(s) print(t) \['s', 'p', 'a', 'm'] \end{pycode} \afterverb % Because {\tt list} is the name of a built-in function, you should avoid using it as a variable name. I also avoid {\tt l} because it looks too much like {\tt 1}. So that's why I use {\tt t}.

The {\tt list} function breaks a string into individual letters. If you want to break a string into words, you can use the {\tt split} method:

\index{split method} \index{method!split}

\beforeverb \begin{pycode}

> > > s = 'pining for the fjords' t = s.split() print(t) \['pining', 'for', 'the', 'fjords'] \end{pycode} \afterverb %

\newpage

An optional argument called a {\bf delimiter} specifies which characters to use as word boundaries. The following example uses a hyphen as a delimiter:

\index{optional argument} \index{argument!optional} \index{delimiter}

\beforeverb \begin{pycode}

> > > s = 'spam-spam-spam' delimiter = '-' s.split(delimiter) \['spam', 'spam', 'spam'] \end{pycode} \afterverb % {\tt join} is the inverse of {\tt split}. It takes a list of strings and concatenates the elements. {\tt join} is a string method, so you have to invoke it on the delimiter and pass the list as a parameter:

\index{join method} \index{method!join} \index{concatenation}

\beforeverb \begin{pycode}

> > > t = \['pining', 'for', 'the', 'fjords'] delimiter = '-' delimiter.join(t) 'pining-for-the-fjords' \end{pycode} \afterverb % In this case the delimiter is a space character, so {\tt join} puts a '-' between words. To concatenate strings without delimiters, you can use the empty string, \verb"''", as a delimiter.

\index{empty string} \index{string!empty}

\section{Objects and values}

\index{object} \index{value}

If we execute these assignment statements:

\beforeverb \begin{pycode} a = 'banana' b = 'banana' \end{pycode} \afterverb % We know that {\tt a} and {\tt b} both refer to a string, but we don't know whether they refer to the {\em same} string. There are two possible states:

\index{aliasing}

\beforefig \centerline{\includegraphics{figs/list1.eps\}} \afterfig

In one case, {\tt a} and {\tt b} refer to two different objects that have the same value. In the second case, they refer to the same object.

\index{is operator} \index{operator!is}

To check whether two variables refer to the same object, you can use the {\tt is} operator.

\beforeverb \begin{pycode}

> > > a = 'banana' b = 'banana' a is b True \end{pycode} \afterverb % In this example, Python only created one string object, and both {\tt a} and {\tt b} refer to it.

\newpage

But when you create two lists, you get two objects:

\beforeverb \begin{pycode}

> > > a = \[1, 2, 3] b = \[1, 2, 3] a is b False \end{pycode} \afterverb % So the state diagram looks like this:

\index{state diagram} \index{diagram!state}

\beforefig \centerline{\includegraphics{figs/list2.eps\}} \afterfig

In this case we would say that the two lists are {\bf equivalent}, because they have the same elements, but not {\bf identical}, because they are not the same object. If two objects are identical, they are also equivalent, but if they are equivalent, they are not necessarily identical.

\index{equivalence} \index{identity}

Until now, we have been using `object'' and` value'' interchangeably, but it is more precise to say that an object has a value. If you execute {\tt \[1,2,3]}, you get a list object whose value is a sequence of integers. If another list has the same elements, we say it has the same value, but it is not the same object.

\index{object} \index{value}

\section{Aliasing}

\index{aliasing} \index{reference!aliasing}

If {\tt a} refers to an object and you assign {\tt b = a}, then both variables refer to the same object:

\beforeverb \begin{pycode}

> > > a = \[1, 2, 3] b = a b is a True \end{pycode} \afterverb % The state diagram looks like this:

\index{state diagram} \index{diagram!state}

\beforefig \centerline{\includegraphics{figs/list3.eps\}} \afterfig

The association of a variable with an object is called a {\bf reference}. In this example, there are two references to the same object. % \index{reference} % An object with more than one reference has more than one name, so we say that the object is {\bf aliased}.

\index{mutability}

If the aliased object is mutable, changes made with one alias affect the other:

\beforeverb \begin{pycode\*}{firstnumber = last}

> > > b\[0] = 17 print(a) \[17, 2, 3] \end{pycode\*} \afterverb % Although this behavior can be useful, it is error-prone. In general, it is safer to avoid aliasing when you are working with mutable objects.

\index{immutability}

For immutable objects like strings, aliasing is not as much of a problem. In this example:

\beforeverb \begin{pycode} a = 'banana' b = 'banana' \end{pycode} \afterverb % It almost never makes a difference whether {\tt a} and {\tt b} refer to the same string or not.

\section{List arguments}

\index{list!as argument} \index{argument} \index{argument!list} \index{reference} \index{parameter}

When you pass a list to a function, the function gets a reference to the list. If the function modifies a list parameter, the caller sees the change. For example, \verb"delete\_head" removes the first element from a list:

\beforeverb \begin{pycode} def delete\_head(lst): del lst\[0] \end{pycode} \afterverb % Here's how it is used:

\beforeverb \begin{pycode}

> > > letters = \['a', 'b', 'c'] delete\_head(letters) print (letters) \['b', 'c'] \end{pycode} \afterverb % The parameter {\tt lst} and the variable {\tt letters} are aliases for the same object. The stack diagram looks like this:

\index{stack diagram} \index{diagram!stack}

\vspace{4ex} \beforefig \centerline{\includegraphics{figs/stack5.eps\}} \afterfig \vspace{4ex}

Since the list is shared by two frames, I drew it between them.

\newpage

It is important to distinguish between operations that modify lists and operations that create new lists. For example, the {\tt append} method modifies a list, but the {\tt +} operator creates a new list:

\index{append method} \index{method!append} \index{list!concatenation} \index{concatenation!list}

\beforeverb \begin{pycode}

> > > t1 = \[1, 2] t2 = t1.append(3) print(t1) \[1, 2, 3] print(t2) None t1 = \[1, 2] t3 = t1 + \[3] print (t3) \[1, 2, 3] t2 is t3 False \end{pycode} \afterverb

This difference is important when you write functions that are supposed to modify lists. For example, this function {\em does not} delete the head of a list:

\beforeverb \begin{pycode} def bad\_delete\_head(t): t = t\[1:] # WRONG! \end{pycode} \afterverb

The slice operator creates a new list and the assignment makes {\tt t} refer to it, but none of that has any effect on the list that was passed as an argument.

%{\color{red} MUST EXPAND ON THIS}

\index{slice operator} \index{operator!slice}

An alternative is to write a function that creates and returns a new list. For example, {\tt tail} returns all but the first element of a list:

\beforeverb \begin{pycode} def tail(t): return t\[1:] \end{pycode} \afterverb % This function leaves the original list unmodified. Here's how it is used:

\beforeverb \begin{pycode}

> > > letters = \['a', 'b', 'c'] rest = tail(letters) print(rest) \['b', 'c'] \end{pycode} \afterverb

\begin{exercise}

Write a function called {\tt chop} that takes a list and modifies it, removing the first and last elements, and returns {\tt None}. Then write a function called {\tt middle} that takes a list and returns a new list that contains all but the first and last elements.

\end{exercise}

\newpage

\section{Debugging} \index{debugging}

Careless use of lists (and other mutable objects) can lead to long hours of debugging. Here are some common pitfalls and ways to avoid them:

\begin{enumerate}

\item Don't forget that most list methods modify the argument and return {\tt None}. This is the opposite of the string methods, which return a new string and leave the original alone.

If you are used to writing string code like this:

\beforeverb \begin{pycode} word = word.strip() \end{pycode} \afterverb

It is tempting to write list code like this:

\beforeverb \begin{pycode} t = t.sort() # WRONG! \end{pycode} \afterverb

\index{sort method} \index{method!sort}

Because {\tt sort} returns {\tt None}, the next operation you perform with {\tt t} is likely to fail.

Before using list methods and operators, you should read the documentation carefully and then test them in interactive mode. The methods and operators that lists share with other sequences (like strings) are documented at \url{docs.python.org/lib/typesseq.html}. The methods and operators that only apply to mutable sequences are documented at \url{docs.python.org/lib/typesseq-mutable.html}.

\item Pick an idiom and stick with it.

Part of the problem with lists is that there are too many ways to do things. For example, to remove an element from a list, you can use {\tt pop}, {\tt remove}, {\tt del}, or even a slice assignment. % To add an element, you can use the {\tt append} method or the {\tt +} operator. Assuming that {\tt t} is a list and {\tt x} is a list element, these are right:

\beforeverb \begin{pycode} t.append(x) t = t + \[x] \end{pycode} \afterverb

And these are wrong:

\beforeverb \begin{pycode} t.append(\[x]) # WRONG! t = t.append(x) # WRONG! t + \[x] # WRONG! t = t + x # WRONG! \end{pycode} \afterverb

Try out each of these examples in interactive mode to make sure you understand what they do. Notice that only the last one causes a runtime error; the other three are legal, but they do the wrong thing.

\newpage

\item Make copies to avoid aliasing.

\index{aliasing!copying to avoid} \index{copy!to avoid aliasing}

If you want to use a method like {\tt sort} that modifies the argument, but you need to keep the original list as well, you can make a copy.

\beforeverb \begin{pycode} copied = t.copy() copied.sort() \end{pycode} \afterverb Alternatively, you can do a copy using slicing: \beforeverb \begin{pycode} copied = t\[:] copied.sort() \end{pycode} \afterverb

In this example you could also use the built-in function {\tt sorted}, which returns a new, sorted list and leaves the original alone. But in that case you should avoid using {\tt sorted} as a variable name!

\end{enumerate}

\section{Glossary}

\begin{vocabulary}\[list:] A sequence of values. \index{list} \end{vocabulary}

\begin{vocabulary}\[element:] One of the values in a list (or other sequence), also called items. \index{element} \end{vocabulary}

\begin{vocabulary}\[index:] An integer value that indicates an element in a list. \index{index} \end{vocabulary}

\begin{vocabulary}\[nested list:] A list that is an element of another list. \index{nested list} \end{vocabulary}

\begin{vocabulary}\[list traversal:] The sequential accessing of each element in a list. \index{list!traversal} \end{vocabulary}

\begin{vocabulary}\[mapping:] A relationship in which each element of one set corresponds to an element of another set. For example, a list is a mapping from indices to elements. \index{mapping} \end{vocabulary}

\begin{vocabulary}\[accumulator:] A variable used in a loop to add up or accumulate a result. \index{accumulator} \end{vocabulary}

\begin{vocabulary}\[augmented assignment:] A statement that updates the value of a variable using an operator like \verb"+=". \index{assignment!augmented} \index{augmented assignment} \index{traversal} \end{vocabulary}

\begin{vocabulary}\[reduce:] A processing pattern that traverses a sequence and accumulates the elements into a single result. \index{reduce pattern} \index{pattern!reduce} \end{vocabulary}

\begin{vocabulary}\[map:] A processing pattern that traverses a sequence and performs an operation on each element. \index{map pattern} \index{pattern!map} \end{vocabulary}

\begin{vocabulary}\[filter:] A processing pattern that traverses a list and selects the elements that satisfy some criterion. \index{filter pattern} \index{pattern!filter} \end{vocabulary}

\begin{vocabulary}\[object:] Something a variable can refer to. An object has a type and a value. \index{object} \end{vocabulary}

\begin{vocabulary}\[equivalent:] Having the same value. \index{equivalent} \end{vocabulary}

\begin{vocabulary}\[identical:] Being the same object (which implies equivalence). \index{identical} \end{vocabulary}

\begin{vocabulary}\[reference:] The association between a variable and its value. \index{reference} \end{vocabulary}

\begin{vocabulary}\[aliasing:] A circumstance where two or more variables refer to the same object. \index{aliasing} \end{vocabulary}

\begin{vocabulary}\[delimiter:] A character or string used to indicate where a string should be split. \index{delimiter} \end{vocabulary}

\newpage

\section{Exercises}

\begin{exercise} Write a function called \verb"is\_sorted" that takes a list as a parameter and returns {\tt True} if the list is sorted in ascending order and {\tt False} otherwise. You can assume (as a precondition) that the elements of the list can be compared with the relational operators {\tt <}, {\tt >}, etc.

\index{precondition}

For example, \verb"is\_sorted(\[1,2,2])" should return {\tt True} and \verb"is\_sorted(\['b','a'])" should return {\tt False}. \end{exercise}

\begin{exercise} \label{exo:anagram}

\index{anagram}

Two words are anagrams if you can rearrange the letters from one to spell the other. Write a function called \verb"is\_anagram" that takes two strings and returns {\tt True} if they are anagrams. \end{exercise}

\begin{exercise} \label{exo:duplicate}

The (so-called) Birthday Paradox:

\begin{enumerate}

\index{birthday paradox} \index{duplicate}

\item Write a function called \verb"has\_duplicates" that takes a list and returns {\tt True} if there is any element that appears more than once. It should not modify the original list.

\item If there are 23 students in your class, what are the chances that two of you have the same birthday? You can estimate this probability by generating random samples of 23 birthdays and checking for matches. Hint: you can generate random birthdays with the {\tt randint} function in the {\tt random} module.

\index{random module} \index{module!random} \index{randint function} \index{function!randint}

\end{enumerate}

You can read about this problem at \url{wikipedia.org/wiki/Birthday\_paradox}, and you can see my solution at \url{thinkpython.com/code/birthday.py}.

\end{exercise}

\begin{exercise}

\index{duplicate} \index{uniqueness}

Write a function called \verb"remove\_duplicates" that takes a list and returns a new list with only the unique elements from the original. Hint: they don't have to be in the same order. \end{exercise}

\begin{exercise} \index{append method} \index{method append} \index{list!concatenation} \index{concatenation!list}

Write a function that reads the file {\tt words.txt} and builds a list with one element per word. Write two versions of this function, one using the {\tt append} method and the other using the idiom {\tt t = t + \[x]}. Which one takes longer to run? Why?

You can see my solution at \url{thinkpython.com/code/wordlist.py}. \end{exercise}

\begin{exercise} \index{reverse word pair}

Two words are a \`\`reverse pair'' if each is the reverse of the other. Write a program that finds all the reverse pairs in the word list. \end{exercise}

\newpage

\begin{exercise} \label{exo:bisection}

\index{membership!bisection search} \index{bisection search} \index{search, bisection}

\index{membership!binary search} \index{binary search} \index{search, binary}

To check whether a word is in the word list, you could use the {\tt in} operator, but it would be slow because it searches through the words in order.

Because the words are in alphabetical order, we can speed things up with a bisection search (also known as binary search), which is similar to what you do when you look a word up in the dictionary. You start in the middle and check to see whether the word you are looking for comes before the word in the middle of the list. If so, then you search the first half of the list the same way. Otherwise you search the second half.

Either way, you cut the remaining search space in half. If the word list has 113,809 words, it will take about 17 steps to find the word or conclude that it's not there.

Write a function called {\tt bisect} that takes a sorted list and a target value and returns the index of the value in the list, if it's there, or {\tt None} if it's not.

\index{bisect module} \index{module!bisect}

Or you could read the documentation of the {\tt bisect} module and use that! \end{exercise}

\begin{exercise} \index{interlocking words}

Two words `interlock'' if taking alternating letters from each forms a new word\footnote{This exercise is inspired by an example at \url{puzzlers.org}.}. For example,` shoe'' and `cold'' interlock to form` schooled.''

\begin{enumerate}

\item Write a program that finds all pairs of words that interlock. Hint: don't enumerate all pairs!

\item Can you find any words that are three-way interlocked; that is, every third letter forms a word, starting from the first, second or third?

\end{enumerate} \end{exercise}
