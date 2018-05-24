---
layout : post
excerpt : Avoid this common errors
aside : true
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



###    POSSIBILITY :
#### YOU MAY HAVE UNZIPPED THE PRETRAINED MODEL.DO NOT UNZIP IT USE IT AS IT IS.


####                 SpanishModel CONTAINS spanish.zip DOWNLOADED FROM PRETRAINED MODEL WEBSITE.
##  ERROR NUMBER 4 :
###    DESCRIPTION :
####               PronunciationAcousticMismatchError: There were phones in the dictionary that
####                  do not have acoustic models:

 
###                  SOMETHING LIKE ABOVE
###    POSSIBILITY :
####                    YOU MAY NOT HAVE GLOBAL PHONE DICTIONARY IN SPANISH
####                  MFA SPANISH G2P MODEL ARE TRAINED ON GLOBAL PHONE
####                  DICTIONARY. MFA WON’T KNOW WHAT PHONE IN THE DICTIONARY
####                  CORRESPOND TO WHAT LABEL IN ACOUSTIC MODEL
