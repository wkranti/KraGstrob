---
layout : post
excerpt : The Alignment Process
---
Lets see next process ,download latest Montreal Force Aligner source code from
Link :- [Montreal Forced Aligner](https://github.com/MontrealCorpusTools/Montreal-Forced-Aligner.git)
Pre-trained model I used is Spanish you can download it from MFA website.
before doing this check whether you have latest python module python 3.x
if not installed that first using sudo apt-get install python3 .
Also you should have pip package above pip3.x.
pip install --upgrade pip
1) Open terminal and change directory to unzipped folder of MFA.
2)Run
{% highlight shell %}
 bin/mfa_align .
 {% endhighlight %}
![mfa_align]({{ "/assets/img/mfa_align.png" | site.baseurl }}){:class="img-responsive"}

Such usage information should be printed out.
If not change directory and follow third step
3)
{% highlight shell %}
cd/path/to/Montreal-Forced-Aligner/thirdparty
{% endhighlight %}
Then Run
{% highlight shell %}
python3 kaldibinaries.py ~/kaldi/root
{% endhighlight %}
![py]({{ "/assets/img/py.png" | site.baseurl }}){:class="img-responsive"}
Now change directory to Montreal-Forced-Aligner and run following command.
![mfa1]({{ "/assets/img/mfa1.png" | site.baseurl }}){:class:"img-responsive"}
It would download all packages mentioned inside requirements.txt.
Now run {% highlight shell %} freezing/freeze.sh{% endhighlight %} there will be
folder created by the name dist change directory to that folder and further
change directory to folder named montreal-forced-aligner and change directory to
 bin this should contain two files mfa_align and mfa_train_and_align .
Now run{% highlight shell %} bin/mfa_align {% endhighlight %}or
{% highlight shell %}
bin/mfa_train_and_align
{% endhighlight %}

from montreal-forced-aligner directory output should be similar to output
message mentioned in step 1.With all steps done under Kaldi compile and Montreal
Aligner setup now is the time to align any given .wav file and .lab file
(which contains transcript of given wav file).

NOTE :>
The wav file mentioned should be atleast 16kHz sampling rate.The aligner ignores
the files having sampling rate below 16kHz. The features that the aligner extracts
are MFCCs dervied from spectra from 0 to 7.8 kHz, so sound files must have
Nyquist frequencies higher than 7.8 kHz.To find a sample rate in a Linux system
 Right click the file, then click "Properties." The sample rate information may
appear in a different tab of the Properties box depending on your Linux
distribution and version. If it doesn't appear in the main tab, look for an
"Audio" or "More Info" tab.

Let’s start aligning.

My Home directory has :


  | FOLDER                           | CONTENTS |
  |:---------------------------------|:---------------------------------------------------------: |
  | Montreal-Forced-Aligner-master   | source code from github   |
  |----
  | MFATestWav                       |  containing .wav and .lab file  (corpus path) |
  |----
  | SpanishDict                      | contains spanish dictionary(dictionary path) |
  |----
  | SpanishModel                     | contains Spanish Model from MFA website in spanish.zip form |
  |----
  |                                  |                                                             |
  {: rules="groups"}                                                    

![mfar]({{ "/assets/img/mfar.png" | site.baseurl }}){:class="img-responsive"}


### First Mono-Phone Training.

### Second Tri-Phone Training.

### Third Speaker-Adapted Tri-Phone Training.

Command is :>
{% highlight shell %}
bin/mfa_train_and_align -t ~/output -v ~/path/to/corpus ~/path/to/dict.txt output_directory
{% endhighlight %}
You can also use other command arguments such as
-s > use to allot number of characters to use to identify speakers.
-t > Temporary directory to use for aligining .(~/Documents/MFA).
-j > Number of jobs to use. (default = 3).
-v > verbose.
-c > Temporary files in ~/Documents/MFA and the output directory will be removed
     prior to aligning. This is good to use when aligning a new dataset, but it
     shares a name with a previously aligned dataset.
-h > Display help message.
-i > ignore.
-q > quiet.

### USING PRETRAINED MODEL:
{% highlight shell %}
bin/mfa_align corpus_directory dictionary_path acoustic_model_path output_directory
{% endhighlight %}
![pret]({{ "/assets/img/pret.png" | site.baseurl }}){:class="img-responsive"}

output.zip contains output acoustic model using mfa_train_and_align .Similarly
we can use pre-trained acoustic model.

Now to check output,in Montreal-Forced-Aligner-master under folder named
spanish/MFATestWav/1.TextGrid
Output of MFA is always in textgrid form ,to check alignment results we use praat.
Praat is used for Speech Analysis,Speech Synthesis,Speech Manipulation,Labelling
and Segmentation,etc.
Our purpose is related to analysis.Lets view output of textgrid.
Run :
![pout]({{ "/assets/img/pout.png" | site.baseurl }}){:class="img-responsive"}

Look you have to include 1.wav file in current directory.
![sp]({{ "/assets/img/sp.png" | site.baseurl }}){:class="img-resonsive"}
![ps]({{ "/assets/img/ps.png" | site.baseurl }}){:class="img-resonsive"}
