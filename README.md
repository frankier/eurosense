# EuroSense

The repository contains some attempted fixes to EuroSense. See
http://lcl.uniroma1.it/eurosense/ for the original. Since the approach here
somewhat unsound: attempting to fix up the corpora after the matter, rather
than fixing the underlying problem, please use at your own risk.

## Obtaining

You can download the processed corpus here:

https://archive.org/details/eurosense-hp.fixed.xml

**--OR--**

You can run the fixing script on the original:

   $ pipenv install
   $ pipenv run fix-eurosense.py pipeline path/to/eurosense.v1.0.high-precision.xml

## Motivation

EuroSense 1.0 has a problem where annotations have the wrong language tag. 

Some quick analysis shows that for sentences without problems:

 1. Annotations tags are grouped by language in the same order as the <text> tags
 2. The <annotation> tags are in the same order as in the text

However, for the problem sentences, often neither are the case. Many,
(but maybe not all) of the problems seem to stem from cognates in
multiple languages being given the incorrect tag.

This script first reorders the cognates and then attempts to fix up the other
problems by referring back to the text for the other annotations which have the
incorrect language tag.

Additionally, some anchors are not present in any texts. In this case the
annotation is (almost?) always duplicated. Finally, there are sometimes empty
<text> tags. These are removed.

## Summary of changes

    Dropped unanchorable annotations: 257
    Reorderings: 3350417
    Problem sentences: 134674
    Total problems: 8247578
    Unfixable problems: 3738
    Removed empty sentences: 32191

## Caveats

The lemmatisation seems to have been performed with respect to the tagged
language, so this might mean the annotations have the incorrect lemmas.

## Licenses

The fixing script is available under the Apache v2 license.

EuroSense itself is available under the [Attribution-NonCommercial-ShareAlike
3.0 Unported (CC BY-NC-SA
3.0)](https://creativecommons.org/licenses/by-nc-sa/3.0/) license.
