---
 layout : post
 title : Generating JSON from alignment.
 excerpt : Step by step Alignment Process.
 feature_image : "https://picsum.photos/2560/600?image=1044"
---

So this is the end of GSOC 2018 third week ,Next week there is evaluation.
These three weeks has been great ,I got so many things to learn from my mentor
Robert Oshshorn.

Here in this post we  will learn about creating JSON file from the alignment
process ,In this process we will use the repository that I made you can clone
it [here](https://github.com/wkranti/Newrepo)

At this point if you have any question about why are we creating files in
JSON format please see my other post [here](https://wkranti.github.io/kragstrob/2018/06/04/From-TextGrid-To-JSON/)

This repository will be named Newrepo-master.I have used the name Newrepo in this
post in place of Newrepo-master . Newrepo-master or Newrepo means the same.  
This repository include
* MFATestWav - An empty directory used in alignment process.
* Models - Directory used to download acoustic model.
* output - Folder Used to store output from Alignment Process.
* outputcsv - Folder Used to store CSV output from TextGrid.
* outputjson - Folder Used to store the final JSON output from the alignment
              process.
* testfiles - Folder contains sample audio and transcript file for alignment.
* align.py  - Alignment script .
* textgrid2csv.py - Python script used to derive csv from textgrid.
* csv2json.py - Python script used to make JSON from CSV.
* spanishdict.txt - Spanish dictionary used in alignment.
* install_models.sh - shell script to install models.

Please make sure directories are named similar to what I have given above
and the directories MFATestWav , Models ,output , outputcsv , outputjson are empty
before aligning , it has .gitignore files in all these directory , delete
this .gitignore files . I have only added them in this directory  because
we can't upload empty directory in git repository, it won't be tracked.

So let's start with the process,after you forked the repository
you will see you have above mentioned folder, please make sure you have all
the necessary folder in repository.

Further your system should have python version greater than 3.x.
Some script mentioned does not support version less than 3.x.

Below given process are needed for checking requirements and fetching models.
There are two process mentioned here
###### 1) Download Linux release mentioned in step 2.(Recommended)
###### 2) Building from source mentioned in step 6.

### Using Linux Release.

1) Since Montreal-Forced-Aligner is build on top of kaldi . Kaldi should be
  compiled first.Detailed steps are mentioned in my post [here](https://wkranti.github.io/kragstrob/2018/05/20/Indispensable-Installation/)

2) Download the latest release of Montreal Force Aligner from [here](https://github.com/MontrealCorpusTools/Montreal-Forced-Aligner/releases/tag/v1.0.0)
  You will see following options when you visit this website

  {% highlight shell %}
      montreal-forced-aligner_linux.tar.gz  93 MB
      montreal-forced-aligner_macosx.zip    45 MB
      montreal-forced-aligner_win64.zip     43.5MB
      Source code (zip)
      Source code (tar.gz)

  {% endhighlight %}

   If you are using linux then click the montreal-forced-aligner_linux.tar.gz
    .When you unzip this files one folder by the name montreal-forced-aligner
   will be created . Directory should look like this.


  {% highlight shell %}
   kranti@kranti:~$ tree -d montreal-forced-aligner
   montreal-forced-aligner
   ├── bin
   ├── lib
   │   └── thirdparty
   │       └── bin
   └── pretrained_models
  {% endhighlight %}

   change the name of montreal-forced-aligner to MFA it should look like this.

   {% highlight shell %}
    kranti@kranti:~$ tree -d MFA
    MFA
    ├── bin
    ├── lib
    │   └── thirdparty
    │       └── bin
    └── pretrained_models
   {% endhighlight %}

3) Now, after renaming add this(MFA folder) to the Newrepo(repository cloned from github)

   It should look like this

   {% gist wkranti/f2e8d7d784752dfd84afddf59474064a %}


   If you want to view detailed file view in directory then view this

   {% gist wkranti/d757abf75edb052c8f2ea5a28557834f %}


4) After doing above process check this command.Change directory to Newrepo/MFA
   and then check the command

    {% highlight shell %}
      kranti@kranti:~/Desktop/Newrepo$ cd MFA     
      kranti@kranti:~/Desktop/Newrepo/MFA$ bin/mfa_align
      kranti@kranti:~/Desktop/Newrepo/MFA$ bin/mfa_align
        usage: mfa_align [-h] [-s SPEAKER_CHARACTERS] [-t TEMP_DIRECTORY]
                            [-j NUM_JOBS] [-v] [-n] [-c] [-d] [-e] [-i]
                           corpus_directory dictionary_path acoustic_model_path
                           output_directory
        mfa_align: error: the following arguments are required: corpus_directory
        , dictionary_path, acoustic_model_path, output_directory

    {% endhighlight %}  


     If this usage message is not printed then there is problem in your installation
     process. Follow from the 6th step.

5) Now it is time to download Spanish model using the shell script.

     {% highlight shell %}

      kranti@kranti:~/Desktop/Newrepo$ ./install_models.sh
      % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                     Dload  Upload   Total   Spent    Left  Speed
    100 14.0M  100 14.0M    0     0  40463      0  0:06:02  0:06:02 --:--:-- 60683
    {% endhighlight %}



If above script doesn't work use this [site](http://montreal-forced-aligner.readthedocs.io/en/latest/pretrained_models.html)
to download the model. Put this file as spanish.zip in Models folder.

{% gist 14a21008528f5471ee716c07f2399518 %}

    If you complete this five steps successfully then no need to follow from 6th
    step.Go directly to 9th step.
    Now only option if this(Above five steps) doesn't work is building from source  

### Building from source (7-8th step)

 6) If downloading montreal-forced-aligner_linux.tar.gz does not work
    download the source code of Montreal-Forced-Aligner from github
    [here](https://github.com/MontrealCorpusTools/Montreal-Forced-Aligner)

 7) After doing 1st step and 6th step follow this steps.

    a) Open a terminal and go to the unzipped folder

       {% highlight shell %}
            cd /path/to/Montreal-Forced-Aligner/thirdparty.
       {% endhighlight %}

    b) Run the  thirdparty/kaldibinaries.py script, pointing it to where Kaldi
       was built (python thirdparty/kaldibinaries.py /path/to/kaldi/root).
    c) Run

         {% highlight shell %}
               pip install -r requirements.txt
         {% endhighlight %}

       to install the requirements for the aligner.
    d) Run the build script via freezing/freeze.sh. There will now be a
       montreal-forced-aligner folder in the dist folder. This folder should
       contain a bin folder with the two executables mfa_align and
       mfa_train_and_align that should be used for alignment.  

      After doing this do the 5th step and then 9th step.   


8) More information on installation is mentioned on this
   [site](http://montreal-forced-aligner.readthedocs.io/en/latest/installation.html)

   I have also made blog post on
   [this](https://wkranti.github.io/kragstrob/2018/05/19/Forced-Alignment/)

##### NOTE
       Models should not be unzipped.It is downloaded as spanish.zip and keep
       is as it is in Models folder.Names are case sensititve.

  9) Now is the time to do alignment
      {% highlight shell %}
                  python3 align.py testfiles/64.wav testfiles/64.lab
      {% endhighlight %}   

{% gist wkranti/b3dc9949b751ccfbb6cddf847b230eb3 %}

       Result can be viewed in above gist.
JSON output can be viewed in outputjson.CSV output can be viewed in outpucsv.
Usually I recommend using Linux release(This is method I followed) . We do not
need to compile any binaries in this we have to use as it is given montreal-
forced-aligner_linux.tar.gz .But when building from source ,it would lead you to
error such as 'fstcompile' not found .This file is included in Linux Release
any many other files you may have to include in the source file as you face any errors.
And some errors are included in
[common errors post](https://wkranti.github.io/kragstrob/2018/05/18/Common-Errors/)

The alignment process used here is for alignment of Spanish data.
You can do alignment process with your Spanish audio files . However
do keep this few things in mind before testing files

* Your files should have sample rate above 16000Hz or at least 16000Hz.
* You can convert the sampling rate like this

  {% highlight shell %}
      ffmpeg -i a.wav -ar 16000 b.wav
  {% endhighlight %}  

   where a.wav is you sample file for changing sampling rate and b.wav is resultant
   file we want for alignment purpose.

 * I assume you have computerized ffmpeg.
 * The audio format should be .wav not .mp3 or any other.To convert the audio
    format from .mp3 or any other format to .wav use the following command

    {% highlight shell %}
      ffmpeg -i c.mp3 -ar 16000 d.wav   
    {% endhighlight %}              

* After converting desired files.Next thing make sure you have transcript files
  for test audio files.
* You can do alignment in any language you just have to modify scripts in
  install_models.sh to download desired models.You would also need dictionary
  for that language and it should be in GlobalPhone format.
  Make changes accordingly in align.py to direct it to the model you have downloaded.
* Dictionary can be made using g2p models . information on this is mentioned
  in my this [post](https://wkranti.github.io/kragstrob/2018/05/18/Generating-Dictionary/)

* I also tried to clone my repository Newrepo from github in order to check if is
  working .Here you can view alignment results.

{% gist wkranti/26f97153949e91f599e9e3f4f330841d %}
