# Activities and exercises

OU-XML supports a range of styled activity types, including *activities*, *exercises*, *SAQ*s and *ITQ*s.

## Activities

Activities have two parts - the activity, and the activity answer.

In `ou0book-theme`, activities are defined as:

````text
```{ou-activity} Activity 1
:timing: 1 hour

Do something...
```
````

```{ou-activity} Activity 1
:timing: 1 hour

Do something...
```

Activities can optionally include an answer:

`````text
````{ou-activity} Activity 2
Do something else...

```{ou-answer}
Here is the second activity answer.

And *more* bits of answer.
```

````
`````

````{ou-activity} Activity 2
Do something else...

```{ou-answer}
Here is the second activity answer.

And *more* bits of answer.
```

````

Ideally we should also have an identifier, not least so we can provide a cross-reference link to the activity.


## Exercises


```{ou-exercise} Exercise 1
:timing: 1 hour

Do something...
```

````{ou-exercise} Exercise 2
:timing: 15 minutes
Do something else...

```{ou-answer}
Here is the second activity answer.

And *more* bits of answer.
```
````

We can also have a discussion block:

````{ou-exercise} Exercise 3
:timing: 15 minutes
Do something else...

```{ou-discussion}
Here is the third exercise discussion.

And *more* bits of discussion.
```
````

Or an answer and a discussion block:

````{ou-exercise} Exercise 4
:timing: 1 hour
Do something else...

```{ou-answer}
Here is the fourth exercise answer.

And *more* bits of answer.
```

```{ou-discussion}
Here is the fourth exercise discussion.

And *more* bits of discussion.
```

````

