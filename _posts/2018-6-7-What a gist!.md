---
layout : post
title : What a Gist!
excerpt : An introduction of gist.
feature_image : "https://picsum.photos/2560/600?image=1079"
---
So,In this post we would be looking at gist , gist can be used to include
images , code-snippets in markdown files. Markdown files allow embedding images
in it.
If you are hosting gh-pages with jekyll , It is useful and easy to embed images
and code snippets so you do not have to insert code in markdown itself
adding this line is enough to direct users to your code-snippets and images
in your gist.You just have to include something like This

    {% highlight text %}
      {% gist  c403eaac31a4cf8dacda49adfdc43910  %}
    {% endhighlight %}

     OR

    {% highlight text %}
      {% gist  wkranti/c403eaac31a4cf8dacda49adfdc43910  %}
    {% endhighlight %}

  wkranti is my username ,paste your username and the gist Id of your desired
  gist.URL of the gist look something like this

     {% highlight text %}
       <script src="https://gist.github.com/wkranti/c403eaac31a4cf8dacda49adfdc43910.js"></script>
     {% endhighlight %}

   The number  c403eaac31a4cf8dacda49adfdc43910 is gist Id.

### How do we create gist?
    * You must have Github account to create gist.
    * Navigate to [gist](https://gist.github.com/)
    * Type name and description of your pages.
    * You have two options here Create public Gist and Secret Gist.
    * If you want to include images in gist , look below after you make
      the gist in comment section , you can see the select and drag option.
      click that option and upload desired images.

  Gist also support GeoJSON files.These maps are displayed in embedded gists,
  so you can easily share and embed maps.

### Mapping GeoJSON files on Github.
  GitHub supports rendering geoJSON and topoJSON map files within GitHub
  repositories. Simply commit the file as you would normally using a .geojson
  or .topojson extension. Files with a .json extension are also supported, but
  only if type is set to FeatureCollection, GeometryCollection, or topology.
  Then, navigate to the path of the geoJSON file on GitHub.com.

  When you click the paper icon on the right, you'll also see the changes made
  to that file as part of a commit.

### Resources
  More information about gist can be found [here](https://help.github.com/articles/about-gists/)

  More information about creating gist can be found [here](https://help.github.com/articles/creating-gists/)

  More information about forking gist can be found[here](https://help.github.com/articles/forking-and-cloning-gists/)
