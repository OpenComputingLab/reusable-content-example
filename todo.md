# To Do

Examples of markdown markup that hasn't yet been mapped over to corresponding OU-XML tags...

## Glossary Items

We can define a glossary term as:

````text
```{glossary}
Glossary term one
  Glossary term one definition is indented
```
````

```{glossary}
Glossary term one
  Glossary term one definition is indented
```

We can then refer to a {term}`Glossary term one` that links to the glossary listing.

```{glossary}
A Glossary term two
  Glossary term two definition is indented
  No blank line

  Blank line

Glossary term three
  Glossary term three defintion
```

## YouTube Video items (sphinx-contrib.youtube)

We can embed video items as:

````text
```{youtube} PmxZywVwhP8
```
````

```{youtube} PmxZywVwhP8
Some text
```

## Video Items (sphinxcontrib.video)

We can embed a video file as:

````text
```{video} resources/test.mp4
```
````

Audio using [`innovationOUtside/sphinxcontrib-ou-xml-tags`](https://github.com/innovationOUtside/sphinxcontrib-ou-xml-tags):

```{ou-audio} resources/test.mp3
asasas asasa
```
