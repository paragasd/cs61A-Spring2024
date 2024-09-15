Discussion 7 | CS 61A Spring 2024
=================================

Discussion 7: OOP[​](https://www.learncs.site/docs/curriculum-resource/cs61a/dis/disc07#discussion-7-oop "Direct link to Discussion 7: OOP")
---------------------------------------------------------------------------------------------------------------------

*   [disc07.pdf](https://www.learncs.site/assets/files/disc07-7a9e6ecb7c727ac249d70072199729e4.pdf)

Pick someone in your group to [join Discord](https://cs61a.org/articles/discord). It's fine if multiple people join, but one is enough.

Now switch to Pensieve:

*   **Everyone**: Go to [discuss.pensieve.co](http://discuss.pensieve.co/) and log in with your @berkeley.edu email, then enter your group number. (Your group number is the number of your Discord channel.)

Once you're on Pensieve, you don't need to return to this page; Pensieve has all the same content (but more features). If for some reason Penseive doesn't work, return to this page and continue with the discussion.

Post in the `#help` channel on [Discord](https://cs61a.org/articles/discord/) if you have trouble.

### Getting Started[​](https://www.learncs.site/docs/curriculum-resource/cs61a/dis/disc07#getting-started "Direct link to Getting Started")
--------------------------------------------------------------------------------------------------------------------

Say your name, another class you're taking besides CS 61A, and something you've practiced for a while, such as playing an instrument, juggling, or martial arts. Did you discover any common interests among your group members?

### Q1: Draw[​](https://www.learncs.site/docs/curriculum-resource/cs61a/dis/disc07#q1-draw "Direct link to Q1: Draw")
------------------------------------------------------------------------------------------------------------------------

The `draw` function takes a list `hand` and a list of unique non-negative integers `positions` that are all less than the length of `hand`. It removes `hand[p]` for each `p` in `positions` and returns a list of those elements in the order they appeared in `hand` (not the order they appeared in `positions`).

Fill in each blank with one of these names: `list`, `map`, `filter`, `reverse`, `reversed`, `sort`, `sorted`, `append`, `insert`, `index`, `remove`, `pop`, `zip`, or `sum`. See the [built-in functions](https://docs.python.org/3/library/functions.html) and [list methods](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists) documentation for descriptions of what these do.

**Discussion Time:** Before writing anything, talk as a group about what process you'll implement in order to make sure the right cards are removed and returned. Try not to guess-and-check! The purpose of discussion is for you to try to solve problems without the help of an interpreter checking your work.

Run in 61A Code

For a list `s` and integer `i`, `s.pop(i)` returns and removes the `i`th element, which changes the position (index) of all the later elements but does not affect the position of prior elements.

Calling `reversed(s)` on a list `s` returns an iterator. Calling `list(reversed(s))` returns a list of the elements in `s` in reversed order.

**Aced it? Give yourselves a hand!**

### Object-Oriented Programming[​](https://www.learncs.site/docs/curriculum-resource/cs61a/dis/disc07#object-oriented-programming "Direct link to Object-Oriented Programming")
---------------------------------------------------------------------------------------------------------------------

A productive approach to defining new classes is to determine what instance attributes each object should have and what class attributes each class should have. First, describe the type of each attribute and how it will be used, then try to implement the class's methods in terms of those attributes.

### Q2: Keyboard[​](https://www.learncs.site/docs/curriculum-resource/cs61a/dis/disc07#q2-keyboard "Direct link to Q2: Keyboard")
------------------------------------------------------------------------------------------------------------------------

**Overview:** A keyboard has a button for every letter of the alphabet. When a button is pressed, it outputs its letter by calling an output function (such as `print`). Whether that letter is uppercase or lowercase depends on how many times the caps lock key has been pressed.

First, implement the `Button` class, which takes a lowercase letter (a string) and a one-argument output function, such as `Button('c', print)`.

The `press` method of a `Button` calls its `output` attribute (a function) on its `letter` attribute: either uppercase if `caps_lock` has been pressed an odd number of times or lowercase otherwise. The `press` method also increments `pressed` and returns the key that was pressed. Hint: `'hi'.upper()` evaluates to `'HI'`.

Second, implement the `Keyboard` class. A `Keyboard` has a dictionary called `keys` containing a `Button` (with its letter as its key) for each letter in `LOWERCASE_LETTERS`. It also has a list of the letters typed, which may be a mix of uppercase and lowercase letters.

**Discussion Time:** Before anyone types anything, have a conversation describing the type of each attribute and how it will be used. Start with `Button`: how will `letter` and `output` be used? Then discuss `Keyboard`: how will `typed` and `keys` be used? How will new letters be added to the list called `typed` each time a `Button` in `keys` is pressed? Call the staff if you're not sure! Once everyone understands the answers to these questions, you can try writing the code together.

Run in 61A Code

**Presentation Time:** Describe how new letters are added to `typed` each time a `Button` in `keys` is pressed. One short sentence is enough to describe how new letters are added to `typed`. When you're ready, send a message to the `#discuss-queue` channel with the @discuss tag, your discussion group number, and the message "Put it on our tab!" and a member of the course staff will join your voice channel to hear your description and give feedback.

### Q3: Bear[​](https://www.learncs.site/docs/curriculum-resource/cs61a/dis/disc07#q3-bear "Direct link to Q3: Bear")
------------------------------------------------------------------------------------------------------------------------

Implement the `SleepyBear` and `WinkingBear` classes so that calling their `print` method matches the doctests. Use as little code as possible and try not to repeat any logic from `Eye` or `Bear`. Each blank can be filled with just two short lines.

**Discussion Time:** Before writing code, talk about what is different about a `SleepyBear` and a `Bear`. When using inheritance, you only need to implement the differences between the base class and subclass. Then, talk about what is different about a `WinkingBear` and a `Bear`. Can you think of a way to make the bear wink without a new implementation of `print`?

Run in 61A Code

Implement a `next_eye` method that returns an `Eye` instance that is closed.

One way to make the bear wink is to track how many times the `next_eye` method is invoked using a new instance attribute and return a closed eye if `next_eye` has been called an even number of times.

### Document the Occasion[​](https://www.learncs.site/docs/curriculum-resource/cs61a/dis/disc07#document-the-occasion "Direct link to Document the Occasion")
------------------------------------------------------------------------------------------------------------------------

Please all fill out the [attendance form](https://docs.google.com/forms/d/e/1FAIpQLSeqlK8l6WkScGr-RHR-kM4p5bnR9cllYrG95fDqPJspSlll7A/viewform) (one submission per person per week).
