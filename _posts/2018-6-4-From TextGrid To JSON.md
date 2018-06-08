---
layout : post
title : From TextGrid To JSON
excerpt : Converting the textgrid file to CSV and then to JSON.
feature_image : "https://picsum.photos/2560/600?image=1063"
---

In this post we would concentrate on creating JSON output from TextGrid.
### Why are we converting textgrid to JSON?
*  In Gentle ,aligned text results are shown in JSON format.
*  When alignment process runs online the output needs to shown via exchanging
   data between a browser and a server, the data can only be text.
*  JSON is text, and we can convert any JavaScript object into JSON, and send
   JSON to the server.
*  We can also convert any JSON received from the server into JavaScript objects.
   This way we can work with the data as JavaScript objects, with no complicated
   parsing and translations.


### Some points about JSON(JavaScript Object Notation).
* It is a way to store information in an organized, easy-to-access manner.
  In a nutshell, it gives us a human-readable collection of data that we can
  access in a really logical manner.
* It also have browser compatibility with familiar browser such as Chrome ,
   Internet Explorer ,FireFox ,Edge ,Mozilla.

### How do we convert textgrid to JSON?
* Before converting textgrid to JSON we need to convert textgrid into CSV.
  After that we can convert CSV into JSON.    

### How do we convert textgrid to CSV?
* Fork [TextGrid To CSV converter](https://github.com/kylerbrown/textgrid.git)
* Do the installation process as directed.
* Navigate to textgrid folder you downloaded from Github in above step.Now open terminal.
  Type this command :
  {% highlight shell %}
     python3 textgrid.py -o textgrid2csv.csv 1.TextGrid
  {% endhighlight %}
* Output csv file will be in output.csv and smaple textgrid file would be 1.TextGrid.
* Output will look like this
  {% highlight text %}
      start,stop,name,tier
      0.76,2.23,asta,word
      2.9,4.5,augar,word
  {% endhighlight %}  
### Converting CSV to JSON
* Now that we have converted textgrid to csv we are one step closer to get the
  JSON file format.
* We would use python to convert CSV into JSON.Below code will convert CSV to JSON.


  {% gist wkranti/e8a9cc00955b8e7bd29cf07ed9ecae77 %}

* Name the above file parser.py .Open terminal and Type
    {% highlight shell %}
         python3 parser.py -i textgrid2csv.csv -o output.json
    {% endhighlight %}
* Output will look something like This
  {% highlight text %}
    [
       {
            "tier": "word",
           "start": "0.76",
           "stop": "2.23",
           "name": "asta"
        },
       {
           "tier": "word",
           "start": "2.9",
           "stop": "4.5",
           "name": "augar"
        }
    ]

  {% endhighlight %}      
* So we converted the given TextGrid file into JSON.
