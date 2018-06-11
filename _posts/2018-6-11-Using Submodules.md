---
layout : post
title : Using Submodules.
excerpt : Brief Overview of Submodules.  
feature_image : "https://picsum.photos/2560/600?image=983"
---

In this post we will learn about frequently used method to include Submodules
in github repository.

##### What are submodules ?
A submodule in a git repository is like a sub-directory which is really a
separate git repository in its own right. This is a useful feature when you
have a project in git which depends on a particular versions of other projects.

Here are some languages and thier dependency management ;

* Perl has CPAN
* PHP has Composer, Packagist and good ol’ Pear
* Python has PyPI
* Ruby has Bundler and Rubygems
* Rust has Crates

And many more examples can be found.

You should have proper version of git.
When you add a submodule in Git, you don't add the code of the submodule to the
main repository, you only add information about the submodule that is added to
the main repository. This information describes which commit the submodule is
pointing at. This way, the submodule's code won't automatically be updated if
the submodule's repository is updated. This is good, because your code might
not work with the latest commit of the submodule, it prevents unexpected behaviour.


##### How do we add submodule ?

{% highlight shell %}
   git submodule add <github-repo-which-you-want-to-include>
{% endhighlight %}  

##### How to get submodule ?

{% highlight shell %}
  git submodule init
  git submodule update

  OR
  git submodule update --init

 {% endhighlight %}

##### How submodules are represented ?

{% highlight shell %}
$ git ls-tree HEAD^{tree}
100644 blob 1e38e022c1c7d27f6dd9b765793087b59d147ef8    .cvsignore
100755 blob 44c881fe25b8dc1413d9195677f492121a3789f0    INSTALL.txt
100644 blob 37312d9a1bcc80ac334547f047a2cece38dd24dc    README
100644 blob 3bb0e8592a41ae3185ee32266c860714980dbed7    Rakefile
040000 tree e326ffb3d697e7ac83fa19d93a8a3305120c719e    app
160000 commit fd91ab69279f1e0cfed53353e64811d5aa9c4b5f    commonlib
040000 tree ae93b14ec7ab01ee33053c32eca340a31ce6449f    config
100644 blob bfc265e33e47ffa9796fe7bb7ae7d1fe7e633593    todo.txt
040000 tree 2999c0a790c0033ad93e312c0bc62ecdc9a18f81    vendor

{% endhighlight %}  

The objects can be of various types, such as “commit”, “tag”, “blob” (file),
 “tree” (directory), etc.  Each commit object points to a tree object which
 represents the state of your source code at that commit

##### How to see status of submodules ?

Running git submodule without arguments defaults to running git submodule status,
which produces a helpful summary of the status of all your submodules.Each line
begins with a space, a ‘+’ or a ‘-‘ which indicate the following things:

 \+   The version checked out in the submodule is different from that specified
     in the super-project. The object name shown is that of the commit that
     the submodule is currently at.

–    The submodule hasn’t been initialized or there’s no repository at the
     submodule path (e.g. if you’ve run  git submodule init but not git
     submodule update, or you’ve later deleted the submodule directory from
     the working tree). The object name shown is the commit that’s specified
     in the super-project.

[space]  The submodule’s HEAD is at the correct version – the object name shown
         is that version.

{% highlight shell %}
90287f0250542be256f67ade4e29a618bf6e688f TrakEM2 (0.7m-227-g90287f0)
+f25db2a43b95480c780d865323fce659a1135c2d VIB (tracer-1.4.0-candidate-849-gf25db2a)
e4d3eb47a8f9d4e62d1f356636652c3ecc739d92 batik (remotes/origin/svn/git-svn@216063-588-ge4d3eb4)9fa7f4d993f57e27e3134b016c7d36fbfd33e34c ij-plugins (9fa7f4d)
7ffa48359cdbf7a47735b719a605ea322c58d694 java/linux (heads/master)
-cc218f05fdc0bb55f40f904d5d1f804e8751d0d2 java/linux-amd64
-4f3964234f4e6fd78247e5e7fad9c8becad53e8f java/macosx-java3d
{% endhighlight %}  

More can be learnt regarding submodules.
