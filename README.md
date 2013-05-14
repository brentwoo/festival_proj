# FESTIVAL code snippets

Festival is a Speech Synthesis System, it uses Scheme.

## Installing


_System Requirements:_

* A UNIX machine
* C++ compiler
* GNU make

Mac OS 10.8 does not come out-of-the-box with a C++ compiler. In the App Store download XCode, and in the Preferences in the Downloads tab, install the Command Line Tools.

_Download the source packges from here:_

* http://festvox.org/festival/downloads.html (North America)
* http://www.cstr.ed.ac.uk/downloads/festival/2.1/ (Europe)

At minimum you need the Festival System source, lexicon distributions appropriate for desired voices, a speech database, and the Edinburgh Speech Tools Library. 

The lexicons support different voices. CMU is required for American English voices, OALD is required for British English voices, and POSLEX is required for both BrE and AmE voices. (Note: OALD is only free for non-commercial use) A list of all available voices is given here (http://festvox.org/docs/manual-1.4.3/festival_24.html#SEC97).

For the default, simple American English male voice, get these files.

* festival-###-release.tar.gz
* festlex_CMU.tar.gz
* festlex_POSLEX.tar.gz
* festvox_kallpc16k.tar.gz 
* speech_tools-2.1-release.tar.gz

Compile, using standard make procedure, the speech tools first, then the fest* files. In the folder where you would like to install Festival (e.g., `cd ~/festival`):

    $ tar xzvf speech_tools-2.1-release.tar.gz
    $ cd speech_tools
    $ ./configure
    $ make all
    $ sudo make install

Back in the main festival directory (`cd ~/festival`) unpack and compile the remaining fest* files with the same sequence of commands:

    $ tar xzvf festlex_CMU.tar.gz
    $ cd festival
    $ ./configure
    $ make all
    $ sudo make install

That should be it. in the festival/festival directory, run the program by typing:

    $ bin/festival

It would be a good idea to add this to your PATH.

## Quick start

* To exit the program:

    \> (exit)

### Get it to talk

* Set the variable `utt1`

    \> (set! utt1 (Utterance Text "Hello world"))

* Synthesizes the utterance

    \> (utt.synth utt1)

* This actually pronounces it. You should hear the content of `utt1` after typing:

    > (utt.play utt1)

* _The above three commands are condensed into one function_:

    > (SayText "your text here")

* Other quick speaking commands

    > (intro)
    $ festival examples/saytime

### First commands

* Read in a text file

    $ festival --tts <file>

* Read in a text file, save as sound

    $ text2wave <file> -o <output.wav>

### Switching voices

All installed voices are found in `festival/lib/voices/`. They are organized by language/region. In the English folder you should find `kal_diphone`, the default voice. To change the voice while in Festival:

    > (voice_VOICE_NAME)

    > (voice_cmu_us_awb_cg)
    > (SayText "I am Canadian.")

If you attempt to change the voice to one that is not installed, you will get the appropriate error message:

    festival> (voice_rab_diphone)
    SIOD ERROR: could not open file /Users/home/festival/festival/lib/dicts/oald/oaldlex.scm
    closing a file left open: /Users/home/festival/festival/lib/voices/english/rab_diphone/festvox/rab_diphone.scm

This this because I did not install the OALD lexicon, so I cannot use the British voices. 

To change the default voice, open up `/festival/lib/siteinit.scm`. You will find a line that looks like

    ;(set! voice_default 'voice_cmu_us_awb_arctic_hts)

Remove the semicolon (uncomment) and change the voice to whichever you want. Make sure that the voice and its required lexicon are installed correctly otherwise Festival will crash on startup.

    (set! voice_default 'voice_cmu_us_slt_arctic_hts)

## Check settings

A list of currently defined phonesets (the list of sets that are used by currently loaded voices) is returned by the function

    (PhoneSet.list)

The name, phones, features and silences of the current phoneset may be accessedwith the function

    (PhoneSet.description nil)

If the argument to this function is a list, only those parts of the phoneset description named are returned. For example

    (PhoneSet.description '(silences))
    (PhoneSet.description '(silences phones))
