# YAAnL

Yet Another Annotation Language - A file format for storing file annotations supporting threaded conversations.

## design considerations

Given that this is intended to be used in an distributed offline review tool,
handling multiple versions of files and any possible text is essential.  It is
also important that comment threading be supported.

The annotations are intentionally stored in a separate file than the file being
annotated as it ensures that any file may be annotated with this format.  We use
hashes and quotes to maintain the link between annotations and the related file.

YAAnL is designed to have semantics similar to YAML, enabling a YAML parser to
parse portions of the text.  It may, however, not maintain full compatibility
with YAML.

An initial, incomplete proto-grammar for the language is:

```
<[fields in yaml]
file-name: <file name>
file-hashes: <numbered list of hashes of contents>>
=====
<[annotation]range: <version>:<start-line> <[?]character>-<end-line> <[?]character>[note:consider xpath syntax]
quote:<quote>
<[fields in yaml][comment]comment-author: <author>
<[?]tags: "<tag>" "<tag>">
text: <content>>
-----
<comment>
=====>
<annotation>
```

This is, of course, highly initial, incomplete, and ill specified.

## Some Related Ideas

* [Annotator annotation storage format](http://docs.annotatorjs.org/en/v1.2.x/annotation-format.html)
* [Everyone's a Critic: The Critic Markup Language Proposal](http://macdrifter.com/2013/02/everyones-a-critic-the-critic-markup-language-proposal.html)

## Parsing Research

* [Principled Parsing for Indentation-Sensitive Languages](https://michaeldadams.org/papers/layout_parsing/) - the language is indentation sensitive, this should help parse it.
* [Indentation-Sensitive Parsing for Parsec](https://michaeldadams.org/papers/layout_parsing_2/)
