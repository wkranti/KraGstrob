---
layout : post
excerpt : Avoid this common errors
aside : true
feature_image : "https://picsum.photos/2560/600?image=579"
---

##  COMMON ERRORS :
#### THIS ERROR DOCUMENT IS FOR DEVELOPER USING MFA IN LINUX,UNIX:
#### FOLLOW ALL THE INSTRUCTION MENTIONED ON MFA WEBSITE.
##  ERROR NUMBER 1:
#### AS MENTIONED ON MFA WEBSITE YOU SHOULD USE PYTHON VERSION 3.X AND PIP
#### THEN USE COMMAND "python3" IN EVERY PROCESS MENTIONED IN BUILDING
#### FROM SOURCE PART.
##  ERROR NUMBER 2:
####    DESCRIPTION :
####        no such file 'fstcompile'
####    POSSIBILITY 1:
####                       YOU MAY NOT HAVE COMPILED KALDI.FOLLOW INSTRUCTION IN TOOLS AND SRC INSTALL FILES.
###    POSSIBILITY 2:
####                     USE LATEST VERSION OF MFA "fstcompile" FILE IS LOCATED IN
####                   "lib/thirdparty/bin".
##  ERROR NUMBER 3:
###    DESCRIPTION :
####                  Exception: The language '/home/kranti/montreal-forced-aligner-
####                  master/pretrained_model/english' is not currently included in the distribution, please
####                 align via training or specify one of the following language names: english.


{% highlight sh %}
kranti@kranti:~/Montreal-Forced-Aligner-master$ bin/mfa_align -t ~/output -v ~/MFATestWav ~/SpanishDict/Spanishdict.txt ~/SpanishModel spanish
Traceback (most recent call last):
  File "aligner/command_line/align.py", line 186, in <module>
    action='store_true')
  File "aligner/command_line/align.py", line 151, in validate_args
    def validate_args(args):
Exception: The language '/home/kranti/spanishmodel' is not currently included in the distribution, please align via training or specify one of the following language names: english.
Failed to execute script align
kranti@kranti:~/Montreal-Forced-Aligner-master$

{% endhighlight %}  
###    POSSIBILITY :
#### YOU MAY HAVE UNZIPPED THE PRETRAINED MODEL.DO NOT UNZIP IT USE IT AS IT IS.

{% highlight sh %}
kranti@kranti:~/Montreal-Forced-Aligner-master$ bin/mfa_align -t ~/output -v ~/MFATestWav ~/SpanishDict/Spanishdict.txt ~/SpanishModel/spanish.zip spanish
Setting up corpus information...  
{% endhighlight %}
####                 SpanishModel CONTAINS spanish.zip DOWNLOADED FROM PRETRAINED MODEL WEBSITE.
##  ERROR NUMBER 4 :
###    DESCRIPTION :
####               PronunciationAcousticMismatchError: There were phones in the dictionary that
####                  do not have acoustic models:


{% highlight sh %}
kranti@kranti:~/Montreal-Forced-Aligner-master$ bin/mfa_align -t ~/output -v ~/MFATestWav ~/SpanishDict/Spanishdict.txt ~/SpanishModel/spanish.zip spanish
Setting up corpus information...
Number of speakers in corpus: 1, average number of utterances per speaker: 1.0
Traceback (most recent call last):
  File "aligner/command_line/align.py", line 186, in <module>
    action='store_true')
  File "aligner/command_line/align.py", line 146, in validate_args
    pretrained_dir = os.path.join(root_dir, 'pretrained_models')
  File "aligner/command_line/align.py", line 88, in align_corpus
    shutil.rmtree(args.output_directory, ignore_errors=True)
  File "aligner/models.py", line 129, in validate
    raise (PronunciationAcousticMismatchError(missing_phones))
aligner.exceptions.PronunciationAcousticMismatchError: There were phones in the dictionary that do not have acoustic models:
Failed to execute script align
kranti@kranti:~/Montreal-Forced-Aligner-master$

  {% endhighlight %}
###                  SOMETHING LIKE ABOVE
###    POSSIBILITY :
####                    YOU MAY NOT HAVE GLOBAL PHONE DICTIONARY IN SPANISH
####                  MFA SPANISH G2P MODEL ARE TRAINED ON GLOBAL PHONE
####                  DICTIONARY. MFA WON’T KNOW WHAT PHONE IN THE DICTIONARY
####                  CORRESPOND TO WHAT LABEL IN ACOUSTIC MODEL
