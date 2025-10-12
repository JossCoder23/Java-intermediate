## The Pattern Class

Java’s `java.util.regex` package contains two vital classes:

* `Pattern` Class
* `Matcher` Class

We’ll start with the `Pattern` class which is what we use to define a pattern we want to find in a string. We create a `Pattern` like so:

```java
Pattern pattern = Pattern.compile("Codecademy");
Pattern pattern = Pattern.compile("codecademy", Pattern.CASE_INSENSITIVE);
```

This method compiles a pattern object in such a way as to designate a given string as the pattern to be used to perform regex operations.

Note the second parameter. It’s optional but contains some useful flags we can set that affect how the regex search is performed. Some examples include:

* `Pattern.CASE_INSENSITIVE` - The case of letters will be ignored when performing a search.
* `Pattern.LITERAL` - Special characters in the pattern will not have any special meaning and will be treated as ordinary characters when performing a search.
* `Pattern.UNICODE_CASE` - Use it together with the `CASE_INSENSITIVE` flag to also ignore the case of letters outside of the English alphabet.

To match a string against a pattern, we need to use the `Matcher` class. We will discuss this in the next exercise.