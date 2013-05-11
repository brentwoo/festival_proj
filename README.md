# FESTIVAL code snippets

Festival is a Speech Synthesis System, it uses Scheme.

## Installing


*System Requirements:*

* A UNIX machine
* C++ compiler
* GNU make

Mac OS 10.8 does not come out-of-the-box with a C++ compiler. In the App Store download XCode, and in the Preferences in the Downloads tab, install the Command Line Tools.

*Download the source packges from here:*

* http://festvox.org/festival/downloads.html (North America)
* http://www.cstr.ed.ac.uk/downloads/festival/2.1/ (Europe)

For a quick start, without needing to configure anything, get these files.

`festlex_CMU.tar.gz`
`festlex_POSLEX.tar.gz`
`festvox_kallpc16k.tar.gz`
`speech_tools-2.1-release.tar.gz`

Compile, using standard make procedure, the speech tools first, then the fest* files. In the folder where you would like to install Festival (e.g., `cd ~/festival):

`$ tar xzvf speech_tools-2.1-release.tar.gz`
`$ cd speech_tools`
`$ ./configure`
`$ make all`
`$ sudo make install`

Back in the main festival directory (`cd ~/festival`) unpack and compile the remaining fest* files with the same sequence of commands:

`$ tar xzvf festlex_CMU.tar.gz`
`$ cd festival`
`$ ./configure`
`$ make all`
`$ sudo make install`

That should be it. in the festival/festival directory, run the program by typing:

`$ bin/festival`

## Quick start

* Set the variable `utt1`

`(set! utt1 (Utterance Text "Hello world"))`

* Synthesizes the utterance

`(utt.synth utt1)

* Actually pronounces it. You should hear it

`(utt.play utt1)

* Alternatively use the Say command

`(Say Text "your text here")`

* read in a text file

`$ festival --tts <file>`

* read in a file, save as sound

`$ text2wave <file> -o <output.wav>`