# Sable, XML for TTS

Instead of just feeding Festival plain text, we can provide it with text that is marked up with Sable to indicate precisely how we want a text spoken.

* [Festial manual: Section 10 on XML/SGML/Sable](http://www.cstr.ed.ac.uk/projects/festival/manual/festival_10.html)
* [SABLE, draft/full specification from Bell Labs](http://www.bell-labs.com/project/tts/sable.html)
* [SABLE + aCSS, spoken web pages](http://www.bell-labs.com/project/tts/csssable.html)
* [SABLE cover page, directory of related links](http://xml.coverpages.org/sable.html)

## Using Sable

Get the example file `twinkle.sable`. At your command prompt you can type the tts command we know to read it in:

    $ festival --tts twinkle.sable

or inside Festival:

    (tts "twinkle.sable" 'sable)

