#Phonesets

Set of symbols, which are defined by features (place of articulation, voicing, etc.). Features are defined within a phoneset. 

##Structure of Phonesets

Main form:

    (defPhoneSet
    	NAME
    	FEATUREDEFS
    	PHONEDEFS)

NAME: name of the set. (e.g., mrpa)
FEATUREDEFS: definition of feature name and possible values.

    (vlength short long diphthong schwa 0) ;; vowel length

PHONEDEFS: list of phone definitions. Phone name and values.

Every phoneset must have a definition for silence. "#" must also be an entry in FEATUREDEFS.

    (PhoneSet.silences '(#))

##Commands for looking up Phonesets

List of sets used by currently loaded voices.

    (PhoneSet.list)

Full description of current phoneset

    (PhoneSet.description nil)

Argument can be list of specfic entries desired
	 
    (PhoneSet.description '(silences))
    (PhoneSet.description '(silences phones))

# Lexicon

Provides pronunciations for words. Every lexicon must be defined in `lib/lexicons.scm` and the lexicons themselves can be found in `lib/dicts/`.

Can have three main parts:

1. Addenda: short. Hand-added words.
1. Compiled lexicon: 10k words. (should be auto generated)
1. Method for dealing with words not in either list.

Example of lexicon definition (found at bottom of `lib/dicts/cmu/cmulex.scm`.

    (lex.create "cmu")
    (lex.set.compile.file (path-append cmulexdir "cmudict-0.4.out"))
    (lex.set.phoneset "radio")
    (lex.set.lts.method 'cmu_lts_function)
    (lex.set.pos.map english_pos_map_wp39_to_wp20)
    (cmulex_addenda)

In order:

1. Lexicon creation statement. Argument is unique name.
1. Pointer to compiled lexicon (Lexicon main part 2)
1. Phone set declaration. Phone set must already be declared in the system.
1. Letter-to-sound rules (Lexicon main part 3)
1. (Optional) Part of speech tag mapping.
1. Addenda, exceptional pronunciations (Lexicon main part 1)

The next sections will go over the three main parts to lexicons, in order. 

## Addenda ##

Addenda are manually added rules that handle known exceptional pronunciations. An example addenda is given in `lib/dicts/cmu/cmulex.scm`: 

    (define (cmulex_addenda)
      (lex.add.entry '("worf" n (((w ao r f) 1))))
      (lex.add.entry '("t" n (((t iy) 1))))
      ...

Addenda adds entries to the *current* lexicon, so the lexicon should be explicitly selected. 


## Lexical entries ##

Three parts

* Head word: word, token. (e.g., 'walk', 'chairs')
* Part of Speech: simple atom (e.g., 'punc', 'n'), or nil.
* Pronunciation: actual pronunciation arbitrary Lisp S-expression.

Example entries

    ( "walkers" n ((( w oo ) 1) (( k @ z ) 0)) )
    ( "present" v ((( p r e ) 0) (( z @ n t ) 1)) )
    ( "monument" n ((( m o ) 1) (( n y u ) 0) (( m @ n t ) 0)) ) 

Disambiguating entries with identical headwords

    ( "lives" n ((( l ai v z ) 1)) )
    ( "lives" v ((( l i v z ) 1)) )

Stress convention: monosyllabic function words have no stress, monosyllabic content words have stress.