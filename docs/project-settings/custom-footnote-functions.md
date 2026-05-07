# Custom footnote functions
If you wish, you can write custom code to decide what kind of footnote is needed in each case. Your code should return one of these values.

- `FootnoteType.ParsingGloss`: Print the parsing and the gloss.
- `FootnoteType.Parsing`: Print the parsing only.
- `FootnoteType.Gloss`: Print the gloss only.
- `FootnoteType.None`: Print no footnote at all.

The default code below can be a guide for what the code should look like. For instance, in the NT canon, if a word is above the frequency threshold, the parsing will only be printed if it is not a present indicative.

## Hebrew Old Testament

```
if (lex_id === 1439638) {
	return FootnoteType.None;
}
if (isVerb) {
	if (belowFrequencyThreshold) {
		return FootnoteType.ParsingGloss;
	} else {
		return FootnoteType.Parsing;
	}
} if (isSubstantive) {
	if (belowFrequencyThreshold) {
		return FootnoteType.ParsingGloss;
	} else {
		return FootnoteType.None;
	}
} else {
	if (belowFrequencyThreshold || isInteroggative) {
		return FootnoteType.Gloss;
	} else {
		return FootnoteType.None;
	}
}
```
(The first line is a bit of a quirk: the “Yah” in “Halleluyah” is its own word in the BHSA dataset, and occurs 49 times. But I don't think it ought to be glossed.)

Here are the variables that are available to you for Hebrew Old Testament words:
```
isVerb: boolean
isSubstantive: boolean
lex_id: number
isInteroggative: boolean
belowFrequencyThreshold: boolean
verbStem: "NA" | "qal" | "piel" | "hif" | "nif" | "pual" | "hit" | "hof" | "hsht" | "pasq" | "hotp" | "nit" | "poal" | "poel" | "htpo" | "peal" | "tif" | "etpa" | "pael" | "haf" | "htpe" | "htpa" | "peil" | "etpe" | "afel" | "shaf"
```

## New Testament
Here is the default code:
```
if (isVerb) {
	if (belowFrequencyThreshold) {
		return FootnoteType.ParsingGloss;
	} else if (!(mood == 'indicative' && tense == 'present')) {
		return FootnoteType.Parsing;
	} else {
		return FootnoteType.None;
	}
} if (isSubstantive) {
	if (belowFrequencyThreshold) {
		return FootnoteType.ParsingGloss;
	} else {
		return FootnoteType.None;
	}
} else {
	if (belowFrequencyThreshold) {
		return FootnoteType.Gloss;
	} else {
		return FootnoteType.None;
	}
}
```
Here are the variables that are available to you for New Testament words:
```
isVerb: boolean
isSubstantive: boolean
tense: "NA" | "present" | "imperfect" | "future" | "aorist" | "perfect" | "pluperfect"
voice: "NA" | "active" | "middle" | "passive"
mood: "NA" | "indicative" | "imperative" | "subjunctive" | "optative" | "infinitive" | "participle"
belowFrequencyThreshold: boolean
```

## Caveats
This should be considered an experimental feature. In particular, if your code contains a bug, you're not going to get an error message about it. It'll just fail.

## Security
Potential malefactors take note: the JavaScript that is entered into these boxes is only ever run in an isolated environment, and with a 100 ms timeout.