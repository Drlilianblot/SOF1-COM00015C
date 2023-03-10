# The while statement

Computers are often used to automate repetitive tasks. Repeating identical or similar tasks without making errors is something that computers do well and people do poorly.

Because iteration is so common, Python provides several language features to make it easier. One is the `for` statement we saw earlier. Another is the `while` statement. Here is a version of the previous script that uses a `while` statement:

{% code lineNumbers="true" %}
```python
word = 'Lilian' 
n = 0 
while n < 1000: 
    print(word) 
    n = n+1 
```
{% endcode %}

Lets consider a script that takes a positive number as input and print a countdown to zero, and then print `'Blastoff.'`. The code for the function is:

{% code lineNumbers="true" %}
```python
n = int(input('Enter a positive integer:')) 
while n > 0: 
    print(n) 
    n = n-1 
print('Blastoff!') 
```
{% endcode %}

You can almost read the `while` statement as if it were English. It means, "While $$n$$ is greater than $$0$$, display the value of $$n$$ and then reduce the value of $$n$$ by $$1$$. When you get to $$0$$, display the sentence 'Blastoff!'".

More formally, here is the flow of execution for a `while` statement:

1. Evaluate the condition, yielding `True` or `False`.
2. If the condition is `False`, exit the `while` statement and continue execution at the next statement.
3. If the condition is `True` , execute the body and then go back to step 1.

This type of flow is called a **loop** because the third step loops back around to the top. A flow-control diagram for a loop is shown below:

<figure><img src="../.gitbook/assets/simple-loop-diagram.png" alt=""><figcaption><p>Flow-control diagram of a simple while loop.</p></figcaption></figure>

The body of the loop should change the value of one or more variables so that eventually the condition becomes false and the loop terminates. Otherwise the loop will repeat forever, which is called an **infinite loop**. An endless source of amusement for computer scientists is the observation that the directions on shampoo, "Lather, rinse, repeat," are an infinite loop.

In the previous case, we can prove that the loop terminates because we know that the value of `n` is finite, and we can see that the value of `n` gets smaller each time through the loop, so eventually we have to get to `0`. In other cases, it is not so easy to tell:

{% code lineNumbers="true" %}
```python
n = int(input('Enter a positive integer:') 
while n != 1: 
    print(n) 
    if n % 2 == 0: # n is even 
        n = n / 2 
    else: # n is odd 
        n = n * 3 + 1 
```
{% endcode %}

The condition for this loop is `n != 1`, so the loop will continue until `n` is `1`, which makes the condition false. Each time through the loop, the program outputs the value of `n` and then checks whether it is even or odd. If it is even, `n` is divided by 2. If it is odd, the value of `n` is replaced with `n*3+1`. For example, if the input is 3, the resulting sequence is 3, 10, 5, 16, 8, 4, 2, 1.

Since `n` sometimes increases and sometimes decreases, there is no obvious proof that `n` will ever reach `1`, or that the program terminates. For some particular values of `n`, we can prove termination. For example, if the starting value is a power of two, then the value of `n` will be even each time through the loop until it reaches `1`. The previous example ends with such a sequence, starting with 16.

The hard question is whether we can prove that this program terminates for _"all positive values"_ of `n`. So far, no one has been able to prove it _or_ disprove it (See [Collatz conjecture](https://www.wikipedia.org/wiki/Collatz\_conjecture))!
