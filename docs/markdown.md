# Markdown

There is support for simple markdown. You can add italics:

```
hello *world*
```

This will be printed as: hello *world*

If you use biblical languages in your note, you should put that in double brackets:


```
this is my language [[θεός]] is a Greek word
```

This will be printed as: this is my language θεός is a Greek word

Why should you bother? Because you want to make sure it uses the correct font. The font you use for your language may not have Greek or Hebrew letters.

To be safe, you can specify that the text is Greek or Hebrew.

```
Genesis starts with the words [[hebrew|בְּרֵאשִׁ֖ית בָּרָ֣א אֱלֹהִ֑ים]] and John starts with the words [[greek|Ἐν ἀρχῇ ἦν ὁ λόγος]]
```

If you want to be safe, always specify Greek or Hebrew. Even if it's Aramaic text, just use `hebrew`.

!!! note "Under the hood"
    Technically, you only need to specify `greek` or `hebrew` if these two things are both true:

    1. The phrase you're quoting has more than one word.
    2. The biblical language has a different text direction from your language. (For instance, English has the same text direction as Greek but a different text direction from Hebrew.)

