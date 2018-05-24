---
layout : post
excerpt : The Alignment Process
feature_image : "https://picsum.photos/200/300?image=547"
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

{% highlight sh %}
kranti@kranti:~/Montreal-Forced-Aligner1$ bin/mfa_align
usage: mfa_align [-h] [-s SPEAKER_CHARACTERS] [-t TEMP_DIRECTORY]
                 [-j NUM_JOBS] [-v] [-n] [-c] [-d] [-e] [-i]
                 corpus_directory dictionary_path acoustic_model_path
                 output_directory
mfa_align: error: the following arguments are required: corpus_directory, dictionary_path, acoustic_model_path, output_directory
kranti@kranti:~/Montreal-Forced-Aligner1$

{% endhighlight %}  
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

{% highlight sh %}
kranti@kranti:~/Montreal-Forced-Aligner1/thirdparty$ python3 kaldibinaies.py ~/kaldi/root

{% endhighlight %}
Now change directory to Montreal-Forced-Aligner and run following command.

{% highlight sh %}
kranti@kranti:~/Montreal-Forced-Aligner-master$ pip install -r requirements.txt
Collecting https://github.com/pyinstaller/pyinstaller/archive/develop.zip (from -r requirements.txt (line 5))
  Downloading https://github.com/pyinstaller/pyinstaller/archive/develop.zip
     - 10kB 33kB/s^Z

{% endhighlight %}  
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


{% highlight sh %}
kranti@kranti:~/Montreal-Forced-Aligner-master$ bin/mfa_train_and_align -t ~/output -v ~/MFATestWav ~/SpanishDict/Spanishdict.txt spanish
Setting up corpus information...
Creating dictionary information...
Setting up training data...
Calculating MFCCs...
Calculating CMVN...
Number of speakers in corpus: 1, average number of utterances per speaker: 1.0
Beginning monophone training...
  0%|                                                                       | 0/39 [00:00<?, ?it/s]log-likelihood -83.4514
skipped transitions 140 183
missing data gaussians 6
  3%|█▌                                                             | 1/39 [00:00<00:13,  2.91it/s]log-likelihood -81.0823
skipped transitions 140 183
missing data gaussians 6
  5%|███▏                                                           | 2/39 [00:00<00:11,  3.21it/s]log-likelihood -81.0169
skipped transitions 140 183
missing data gaussians 6
  8%|████▊                                                          | 3/39 [00:00<00:10,  3.46it/s]log-likelihood -80.9504
skipped transitions 140 183
missing data gaussians 6
 10%|██████▍                                                        | 4/39 [00:01<00:09,  3.65it/s]log-likelihood -80.3842
skipped transitions 140 183
missing data gaussians 6
{% endhighlight %}

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

{% highlight sh %}
kranti@kranti:~/Montreal-Forced-Aligner-masters bin/mfa_align -t ~/align -v ~/MFATestHav ~/Spanis
hDict/Spd2.txt ~/SpanishModel/output.zip spanish

Setting up corpus information...

Number of speakers in corpus: 1, average number of utterances per speaker: 1.0

Creating dictionary information...

Setting up training data...

Calculating MFCCs...

Calculating CMVN...

Number of speakers in corpus: 1, average number of utterances per speaker: 1.0

Done with setup.
There were words not found in the dictionary

100%

| 2/2 [oo:oo<oo:oo, 2.43it/s]
Done! Everything took 5.192259311676025 seconds
kranti@kranti:~/Montreal-Forced-Aligner-masters I

Would ou like to abort to fix them? (Y N)n

{% endhighlight %}

output.zip contains output acoustic model using mfa_train_and_align .Similarly
we can use pre-trained acoustic model.

Now to check output,in Montreal-Forced-Aligner-master under folder named
spanish/MFATestWav/1.TextGrid
Output of MFA is always in textgrid form ,to check alignment results we use praat.
Praat is used for Speech Analysis,Speech Synthesis,Speech Manipulation,Labelling
and Segmentation,etc.
Our purpose is related to analysis.Lets view output of textgrid.
Run :

{% highlight sh %}
kranti@kranti:~/Montreal-Forced-Aligner-master$ praat --open 1.TextGrid 1.wav
{% endhighlight %}  

Look you have to include 1.wav file in current directory.
