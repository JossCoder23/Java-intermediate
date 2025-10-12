## Introduction to Regex

Have you ever wondered how search engines like Google Search can interpret the text you type and return results accurately to your inquiry?

Aside from the higher-level steps of crawling, indexing, and ranking, and also ignoring the layers of machine learning behind the information Google has at its disposal, Google, and any other search engine needs a way to interpret and use what you type. It needs to functionally accept whatever you put into that search bar and return results. This process poses the following question:

“How do I generalize all possible inputs but still retain accuracy and precision in the results?”

The answer is regular expressions,  or regex for short.

A regex is a pattern represented by a sequence of characters. They’re used in search engines, word processors, text editors, and many other places due to their general use cases and base functionality. Many programming languages provide regex capabilities either from libraries or built straight into the language. Java is one such language that has an entire package dedicated to regex.

In the simplest sense, regex can be used to perform text search and text replace operations. It’s always first represented as a search pattern, which is used to define what exactly is being searched for when scanning text. Many unique ways were developed to add as much utility and specification as possible when creating search patterns. In all regards, search patterns put an emphasis on precision despite the “catch-all” genericness it has to consider.

Regex can be broken into the following categories:

* Character classes and Capture Groups
* Escaped Characters
* Quantifiers
* Alternation

We’re going to learn about these categories and how to read, write, and manipulate regex search patterns in Java. Java doesn’t have a built-in regex class, so we import a java.util.regex package to work with regular expressions.

Let’s start with talking about this java.util.regex package and how it implements regex!