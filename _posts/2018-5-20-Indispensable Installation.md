---
 layout : post
 title : Indispensable Installation
 excerpt : Get Started
---

This blog is about running pre-trained Spanish model using Montreal Force
 Aligner.In this tutorial I will be using Ubuntu 16.04lts.Let’s get started.
Download Kaldi.
Link :-[Github]( https://github.com/kaldi-asr/kaldi.git)
Compile Kaldi :- More information about compiling Kaldi is given in tools and
 src directory under the green icon named “INSTALL”.
First follow instruction in tools section and then under src section.
First step is to check dependencies.
Command >
{% highlight shell %}
extras/check_dependencies.sh
{% endhighlight %}

Such message should be printed out.This script checks extra dependencies needed
for kaldi.If your system default C++ compiler is not supported, you can do the
check with another compiler by setting the CXX environment variable, e.g.
{% highlight shell %}
CXX=g++-4.8 extras/check_dependencies.sh
{% endhighlight %}
Then run
Command >
{% highlight shell %}
        make
{% endhighlight %}        
This command installs various libraries to support kaldi features such as ATLAS
,openfst,SCTK,sph2pipe and CLAPACK headers.
If your system default compiler does not have adequate support for C++11, you
can specify a C+11 compliant compiler as a command argument, e.g.
{% highlight shell %}
make CXX=g++-4.8
{% endhighlight %}
If you have multiple CPUs and want to speed things up, you can do a parallel
 build by supplying the "-j" option to make, e.g. to use 4 CPUs
{% highlight shell %}
make -j 4
{% endhighlight %}
Look you should be in tools directory in kaldi.
Now change your working directory to src
The installation instructions are
{% highlight shell %}
./configure --shared
make depend -j 8
make -j 8
{% endhighlight %}
Note that we added the "-j 8" to run in parallel because "make" takes a long
time. 8 jobs might be too many for a laptop or small desktop machine with not
many cores.
For any further information visit [Kaldi](http://kaldi-asr.org/doc/)
and head straight to "The build process (how Kaldi is compiled)".
With all this processes done.We have completed process of compiling Kaldi.
We would align using pre-trained models available on Montreal Force Aligner
Download source code from github.
