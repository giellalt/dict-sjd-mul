=============
Current tasks
=============

after meeting with Cip 2016-04-25 (topic "sort order")
-->remove underscore in entries
-->think about sort order of non-letters, ! , - 1 2 space etc.

=======
General
=======

This directory contains lexical material relevant to Kildin Saami. The /src directory contains the data in gtdictionary format (with some adaptations to be explained elsewhere) and is linked to a scheme (found in ../scripts/dictionary.dtd) in order to format it if read by a web browser. 

Incoming files are in the /inc directory. The incoming data includes (or will include) Kildin Saami lexical items collected from:
*fieldnotes (Kola Saami Documentation Project, 2004+) (spoken) sjd
*dictionary Itkonen 1958 (spoken) sjd
*dictionary Afanas'eva et al. 1985 (written) sjd-rus
*dictionary Kert 1986 (written) sjd-rus
*dictionary Kert 1986 (written) rus-sjd
*dictionary Sammallahti et al. 1991 (written) sjd-sme
*dictionary Sammallahti et al. 1991 (written) sme-sjd
*dictionary Eliseev et al. 2007 (spoken) sjd
*dictionary Antonova 2014 (written) sjd-rus
*teaching materials Antonova 1982 (written) sjd-rus
*teaching materials Šaršina et al. 2008 (written) sjd-rus
*phrase book Afanas'eva 2010 (written) sjd-rus

The goal is to merge all incoming lemmas into one new dictionary. /src is the destination directory for the evolving new dictionary entries.

For each letter we create a separate file. Additional files might be needed for bound morphemes (suffixes, clitics, etc.) and for multiword expressions listed as lemmas in the original data. A final solution for handling these lemmas will be found during our ongoing work.

The current goal is to unify the data in the files
*sjd2x-а.xml
*…
*sjd2x-т.xml
and move them into /scr once they are finished.

=======================================
Instruction how to proceed (for Sirrke)
=======================================
--------------------------------
A Dealing with the incoming data
--------------------------------

1) Оpen these two incoming files:
*sjd2x/inc/kurutch1985_sjdrus.xml
*sjd2x/inc/sjd2x-incoming.xml
(not the other files, I will clean up them myself)

2) Тake from these two files all dictionary entries (i.e. <e/>, see below) where the lemma (<l/>) starts with the letter а

3) Move these entries into the file:
*sjd2x/sjd2x-а.xml
It is not important where in the file you put it, it can be in the beginning or the end or somewhere between other dictionary entries. We will later use a script to sort the entries alphabetically. I will show you this script later.

4) Validate the XML syntax in all three files after the changes and if everything is all right commit the changes in all three files to SVN, i.e. commit the new version of the files in /sjd2x/inc with removed entries and the files in /sjd2x with added entries.

5) Continue with the letters б, в, г, etc. (note that some letters are already finished). If the file for the respective letter does not exist yet, create a new file for it in /sjd2x.

6) Once this task is finished, the old files in /inc
*sjd2x/inc/kurutch1985_sjdrus.xml
*sjd2x/inc/sjd2x-incoming.xml
will be empty and can be removed from SVN.

--------------------------------
B Merging the content of entries
--------------------------------

1) The next step is to search for doublets in the newly created files and merge the content of these doublets by removing obsolete information. I will explain more when we have come closer to the end of working step A.

-----------------------
C Finalizing the merger
-----------------------

1) The next step is to move the newly created files into the final directory /src and to finalize the lexicographic structure, incl. adding/correcting in the XML markup in order to fullfill the XML scheme (found in ../scripts/dictionary.dtd) as well as adding/correct translations, grammatical information, etc. I will explain more when we have come closer to the end of working step B.

==========================================
Explanation of the XML markup (for Sirrke)
==========================================
------
Fields
------
<r/> "root", i.e. the whole dictionary

<e/> "entry", i.e. one dictionary entry, incl. lemma, grammatical information, meaning, etc.

<lg/> "lemma group", i.e. all information belonging to one lemma

<l/> "lemma"; i.e. the Kildin Saami word to be explained in the dictionary; the lemma is presented in the spelling preferred by the Kola Saami Documentation Project, in most (but not all!) cases this spelling is similar to kuru1985

<orth/> "orthography group"; comprising alternative orthographic spellings found in the source data

<lvar/> "lemma variant", i.e. variant spellings found in the dictionaries or other written sources

<infl/> "inflection group"; comprising information on inflection class, stem gradation or other morphologically relevant clues

<mg/> "meaning group", i.e. all information belonging to the explanation/translation of the meanin or meanings of one lemma; one meaning group for each meaning (words can have several meanings!)

<lexg/> "lexicon group" lexicon-like explanation (rather than true translation)

<tg/> "translation group", one translation group for each translation (one and the same meaning can have several translations!) 

<xg/> "example group"

<x/> "example"

<xtg/> "example translation group"

<xt/> "example translation"

…to be completed…

----------
Attributes
----------
pos= part of speech (часть речи): A (adjective), Adv (adverb), Cc (coordinator), Cs (subordinator), Det (determiner), N (noun), Phrase_N (noun phrase), Phrase_V (verb phrase), Phrase_S (sentence), Pro (pronoun), V (verb), etc.

==========================================
Explanation of scripts we use (for Sirrke)
==========================================

all script live in /sripts
you run the scripts from the command line

----------------------
Sorting alphabetically
----------------------
1) use this command for sorting in the preliminary files (like for instance /sjd2x/sjd2x-т.xml):
xsltproc --param sortlang 'ru' scripts/sort-dict.xsl sjd2x-т.xml > sjd2x-т-sorted.xml
2) check if everything looks all right in the new file
3) remove sjd2x-т.xml
4) rename sjd2x-т-sorted > sjd2x-т.xml
5) commit the new version of sjd2x-т.xml to SVN

==================================
Kildin Saami alphabet (sort order)
==================================
all possible (small) letters of all known orthography variants are included
а а̄ ӓ б в г д е е̄ ё ё̄ ж з һ ʼ и ӣ й ј ҋ к л ӆ м ӎ н ӊ ӈ о о̄ ӧ п р ҏ с т у ӯ ӱ ф х ц ч ш щ ъ ы ы̄ ӹ ь ҍ э ӭ ю ю̄ я я̄

capital letters are _not_ sorted vs small letters

=====================
Unicode issues
=====================
always check:
*combined vs. precomposed CYRILLIC LETTER Е WITH DIAERESIS
*combined vs. precomposed CYRILLIC LETTERS И, У WITH MACRON
*CYRILLIC LETTER SHHA (not Latin h)
*Cyrillic vowel letters (not Latin ones)
more possible issues
*CYRILLIC SMALL LETTER ю plus MACRON (not е plus diaresis plus macron)
*COMBINING OVERLINE (not COMBINING MACRON)
*two combining macron on each other
*latin capital T (instead of cyrillic)


THE FOLLOWING ARE OLD NOTES, WHICH HAVE TO BE UPDATED OR REMOVED IF THEY ARE OBSOLETE.

====================
Building the dictionary:
====================
Here is the list of the attribute values for the attribute 'meta'
on the e-element in the xml files:

01 - this is the list of sjdoahpa lemmata that kindly have been corrected by native speaker A.A.Antonova via Elli
-orthography is A.A.Antonova's

02 - Michas Liste downloaded from MPI server
-The list from MPI is the basis of dict extention: the infos from the list in pseudo-rtf format should be incorporated gradually.
-orthography is Kuruč's

03 - short word list from Lazer kallsa moajjnas created by Micha, about somewhat more than 100 words
-the Unicode of Latin vs. Cyrillic is not yet checked
-orthography is Kuruč's

04 - short list of animal names and words related to animals collected by Andrey Dubovcev and Micha, somewhat more than 120 words
-please keep the class-attribute and the semantic info, even though it is incomplete and needs better structuring
-both orthographies (where already included in the imported Excel-chart)

05 - data from the (preliminary) restructered Chaos-Kurutch-file in GT-xml structure
-Placeholders: <SAEX> = Saami example, <SAEXRUTRANSL> =Russian translation of Saami example, <RUTRANSL> =Russian translation of headword, <STEM> =weak stem form (needs to be merged into the element <kur_flex>xxx</kur_flex>)
-das Element <kur_ID> ist eine ID für jedes Lemma, dass in der Originaldatei enthalten war. Ich möchte es behalten, damit man das Wörterbuch eventuell später zu der Originaldatei zuordnen kann.
-das Element <kur_flex>  zeigt den Stufenwechsel, so wie Kurutch ihn analysiert hat. Das ist in den meisten Fällen richtig. Ich will es erstmal behalten und später sehen, was ich damit machen kann. This element also includes Kurutch's inflexion classes as attributes. Die Klassen sind in vielen Fällen nicht richtig. Aber ich will es erstmal behalten. Ich bin gerade dabei, einen eigene Analyse aller Flexionsklassen aufzuschreiben.
-das Element <kur_link> zeigt die Grundform bei abgeleiteten Lemmata
-das Attribute nonceform="*" zeigt, dass dieses Wort einfach nur aus dem Russischen genommen ist. Diese Info ist nicht von Kurutch! Ich habe die Idee dafür aus einem anderen Wörterbuch.
-Es gibt zusätzlich zur alten sjdrus-Struktur eine Example-Gruppe und manchmal auch zusätzliche Kommentare zu den Übersetzungen. Es war mir dabei wichtig, dass ich keine Informationen aus der Originaldatei wegwerfe. Vieles muss aber noch besser strukturiert werden.
-the element <lexicon> contains longer, lexicon-type explanations of cultural items; in Kurutch's dictionary, such explanations are always given in parentheses after the translation
-the element <comment> (under <tg>) includes several preliminary kinds of attributes (all included in the original dictionary):
--<comment type="aktionsart">
--<comment type="explan">
--<comment type="понуд."> yet unclear how to scope with that kind of comment
--<comment type="compare">то же, что = variant of (!aber nicht immer!)
I don't know yet how to deal with them

06 - words added by Micha

=====================
Notes (MR)
=====================
possible problems in the list 01:
 -too many multi-word-expressions for Kildin head-words (e.g. non-lexicalized нызан олма, вӣллькесь роавас ча̄дзь)?
 -also perhaps too many multi-word-expressions for Russian translations?
 -some Kildin verbs are inconsequently translated with either the Russian perfective or imperfective verb (perhaps, the translation should always include both forms tagged as глаг.несв. and глаг.св. [or the like] respectively?)
 -we have to deal consistently with the meaning groups (in case of multiple translations)

 -some spelling variants could be unified (e.g. та̄ррьмъя : та̄ррмъя, е̄ммьнэ : е̄ммьне), but note that these are inconsistencies (mistakes?) in spelling which have nothing to do with the two competing orthographic variants!
 --MR: seems to be fixed already 
 -some Kildin adjectives are inconsequently translated with either the Russian attributive or predicative adjective (perhaps, the translation should always include both forms tagged as прилаг.опред. and прилаг.сказ. [or the like] respectively?)
 --MR: seems to be fixed already
 –several inflected forms (e.g. plural) occur as new entries (as lemmata on their own)
 --MR: seems to be fixed already
 
 
====================
POS mapping
====================
Preliminary list of PoS used in gtdict_sjdrus in Russian and English
This List will be extended during continuing work
Where should it live finally?
глаг.	verb
мест.	pronoun
нареч.	adverb
послел. postposition
предл.	preposition
прилаг.	adjective
прилаг.опред.	attributive adjective
прилаг.сказ.	predicative adjective
прич.	participle
част.	particle
числ.	numeral
числ.неопрeд. indefinite pronoun
с.	connector
сказ. predicate
собст.	proper noun
сущ.	noun

----------------
phrases, e.g.:
mwe._NP: сущ. сущ.
mwe._AP: нареч. прилаг.
mwe._VP: глаг. мест.
mwe._AdP: предл. мест.
----------------


=======================
nonceforms (Russian words for which a !recommended alternative Saami form exists), marked with asterisk like in:
<l src="kur" pos="сущ." nonceform="*">авгусст</l>
But perhaps we should find another convention here?



===========================================================
Orthography issues / Coping with different graphic variants
===========================================================
Value list of the attribute :
kur = Kuruč et al. 1985
aaa = A.A.Antonova

NB: Sjd Oahpa should be changed accordingly wrt. the different
spelling variation, too!

-src="kur" means "according to the orthographic principles of the 1985 dictionary" and concerns mainly the spelling of j and һ (obs! not all words with src="kur" in sjdrus are really listed in the 1985 dictionary)
-<graph_var src="aaa"> means "according to A.A.Antonova's own orthographic principles" and concerns mainly the spelling of йхх and хх (instead of j and һ) but often also other spellings different from both 1985 and (Kert's) 1986 dictionary
-<graph_var src="aaa"> can (hopefully) be derived automatically from src="kur" (see the rules below)
-all derivations aaa --> kur (which cannot be done automatically [because of underspecification]) have therefore by checked manually by Micha
-all entries missing an src="..." attribute have similar spellings in kur and aaa

-----------------
kur -> aaa mapping:
-----------------

REGELN FÜR UMWANDLUNG DER GRAPHISCHEN VARIANTEN KUR (Kuruč 1985) --> AAA (=A.Antonovas Orthographie)
Beachte Reihenfolge!
1) stimmloses /j/
1a) jj_# --> хxь_# (=Buchstabenkombination <jj> im Wortauslaut wird ersetzt durch Buchstabenkombination хxь)
1b) j_# --> xь_# (=Buchstabe <j> im Wortauslaut wird ersetzt durch Buchstabenkombination хь)
1c) jj_C --> xь (=Buchstabenkombination <jj> vor einem der Buchstaben <к, п, т, ц, ч> wird ersetzt durch Buchstabenkombination xь)
1c) j_C --> й (=Buchstabe <j> vor einem der Buchstaben <к, п, т, ц, ч> wird ersetzt durch Buchstabenkombination xь)

2) Präaspiration
2a) һ_Cь_# --> ххь_C_# (=Buchstabe <һ> vor einem der Buchstaben <к, п, т, ц, ч> vor dem Buchstaben <ь> wird ersetzt durch Buchstabenkombination <хxь>; der Buchstabe <ь> im Wortauslaut wird gelöscht)
2b) һ_Cҍ_# --> ххь_C_# (=Buchstabe <һ> vor einem der Buchstaben <к, п, т, ц, ч> vor dem Buchstaben <ҍ> wird ersetzt durch Buchstabenkombination <хxь>; der Buchstabe <ҍ> im Wortauslaut wird gelöscht)
2d) һ_C_ё --> ххь_C__ (=Buchstabe <һ> vor einem der Buchstaben <к, п, т, ц> vor dem Buchstaben <ё> wird ersetzt durch Buchstabenkombination <хxь>; der Buchstabe <ё> wird zum Buchstaben <э>)
2c) һ_C_е --> ххь_C__ (=Buchstabe <һ> vor einem der Buchstaben <к, п, т, ц> vor dem Buchstaben <е> wird ersetzt durch Buchstabenkombination <хxь>; der Buchstabe <е> wird zum Buchstaben <э>)
******* der Rest müsste bei der Reihenfolge egal sein ******* 
2e) һ_C_я --> ххь_C_# (=Buchstabe <һ> vor einem der Buchstaben <к, п, т, ц> vor dem Buchstaben <я> wird ersetzt durch Buchstabenkombination <хxь>; der Buchstabe <я> wird zum Buchstaben <а>)
2f) һ_C_ӓ --> ххь_C_# (=Buchstabe <һ> vor einem der Buchstaben <к, п, т, ц> vor dem Buchstaben <ӓ> wird ersetzt durch Buchstabenkombination <хxь>; der Buchstabe <ӓ> wird zum Buchstaben <а>)
2g) һ_C_ю --> ххь_C_# (=Buchstabe <һ> vor einem der Buchstaben <к, п, т, ц> vor dem Buchstaben <ю> wird ersetzt durch Buchstabenkombination хxь; der Buchstabe <ю> wird zum Buchstaben <у>)
2h) һ_ч --> ххь_ч (=Buchstabe <һ> vor dem Buchstaben <ч> wird ersetzt durch Buchstabenkombination <хxьч>)
2i) һ_C --> ххь_C (=Buchstabe <һ> vor einem der Buchstaben <к, п, т, ц> wird ersetzt durch Buchstabenkombination <хxь>)


REGELN FÜR UMWANDLUNG DER GRAPHISCHEN VARIANTEN KUR (Kuruč 1995) --> AAA (=A.Antonovas Orthographie)
1) stimmloses /ҋ/
1a) ҋҋ_# --> хxь_# (=Buchstabenkombination <ҋҋ> im Wortauslaut wird ersetzt durch Buchstabenkombination хxь)
1b) ҋ_# --> xь_# (=Buchstabe <ҋ> im Wortauslaut wird ersetzt durch Buchstabenkombination хь)
1c) ҋҋC --> xь (=Buchstabenkombination <ҋҋ>+<к, п, т, ц, ч> wird ersetzt durch Buchstabenkombination xь)
1d) ҋC --> й (=Buchstabenkombination <ҋ>+<к, п, т, ц, ч> wird ersetzt durch Buchstabenkombination xь)

2) Präaspiration
2a) '_Cь_# --> ххь_C_# (=Buchstabe <'> vor einem der Buchstaben <к, п, т, ц, ч> vor dem Buchstaben <ь> wird ersetzt durch Buchstabenkombination <хxь>; der Buchstabe <ь> im Wortauslaut wird gelöscht)
2b) '_Cҍ_# --> ххь_C_# (=Buchstabe <'> vor einem der Buchstaben <к, п, т, ц, ч> vor dem Buchstaben <ҍ> wird ersetzt durch Buchstabenkombination <хxь>; der Buchstabe <ҍ> im Wortauslaut wird gelöscht)
2d) '_C_ё --> ххь_C__ (=Buchstabe <'> vor einem der Buchstaben <к, п, т, ц> vor dem Buchstaben <ё> wird ersetzt durch Buchstabenkombination <хxь>; der Buchstabe <ё> wird zum Buchstaben <э>)
2c) '_C_е --> ххь_C__ (=Buchstabe <'> vor einem der Buchstaben <к, п, т, ц> vor dem Buchstaben <е> wird ersetzt durch Buchstabenkombination <хxь>; der Buchstabe <е> wird zum Buchstaben <э>)
******* der Rest müsste bei der Reihenfolge egal sein @cip: stimmt nicht ganz!*******  
2e) '_C_я --> ххь_C_# (=Buchstabe <'> vor einem der Buchstaben <к, п, т, ц> vor dem Buchstaben <я> wird ersetzt durch Buchstabenkombination <хxь>; der Buchstabe <я> wird zum Buchstaben <а>)
2f) '_C_ӓ --> ххь_C_# (=Buchstabe <'> vor einem der Buchstaben <к, п, т, ц> vor dem Buchstaben <ӓ> wird ersetzt durch Buchstabenkombination <хxь>; der Buchstabe <ӓ> wird zum Buchstaben <а>)
2g) '_C_ю --> ххь_C_# (=Buchstabe <'> vor einem der Buchstaben <к, п, т, ц> vor dem Buchstaben <ю> wird ersetzt durch Buchstabenkombination <хxь>; der Buchstabe <ю> wird zum Buchstaben <у>)
2h) '_ч --> ххь_ч (=Buchstabe <'> vor dem Buchstaben <ч> wird ersetzt durch Buchstabenkombination <хxьч>)
2i) '_C --> ххь_C (=Buchstabe <'> vor einem der Buchstaben <к, п, т, ц> wird ersetzt durch Buchstabenkombination <хxь>)

Beachte: 
ҋ und j sind graphische Varianten, in den aktuellen rusa-saru kommt nur ҋ vor, aber diese Regeln können wir auch für spätere Dokumente verwenden
һ und ' (Apostroph) sind graphische Varianten, in den aktuellen rusa-saru kommt nur һ vor, aber diese Regeln können wir auch für spätere Dokumente verwenden

-----------------
aaa-> kur mapping:
-----------------
This question is answered now: This mapping is not possible due to underspecification!

-----------------------------
Sorting entries in the files:
-----------------------------
1.
Using the parametrized script from the gtsvn/words/dicts/script (alphabetical sorting of lemmata according to the
alphabet of the language used as parameter):

from the gtsvn/words/dicts/sjdrus/src:
xsltproc --param sortlang 'ru' ../../scripts/sort-dict.xsl sjdrus_mpi.xml > sorted_sjdrus_mpi.xml

@cip added the sorted file for Michal to check the correctnes (sorted using Russian!!!)
@cip: When looking only at the first and the last entries, I got a weird feeling.

2.
sorting by pos (@cip hast to write a small script)

3.
sorting by some other info (meta01, etc.): see 2.!

Test
