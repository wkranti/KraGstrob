---
layout : post
excerpt : Dictionary Generating Process
feature_image : "https://picsum.photos/2560/600?image=564"
---

## Generating dictionary

#### To generate dictionary using g2p models ,download specific g2p model to create dictionary.I have downloaded spanish g2p model.


{% highlight sh%}
kranti@kranti:~/Montreal-Forced-Aligner-master$ bin/mfa_generate_dictionary -t ~/output ~/SpanishModel/spanish_g2p.zip ~/MFATestWav output
Setting up corpus information...
kranti@kranti:~/Montreal-Forced-Aligner-master$
  {% endhighlight %}
View result in output file.There should be two folders corpus and G2P.
In G2P file you will find words.txt in folder spanish_g2p.Open the text file you will find transcript of your wav file.
In such way you can create dictionary of any language using this g2p models.you can also take large training set and create
transcript and use it as dictionary in testing any given file.
