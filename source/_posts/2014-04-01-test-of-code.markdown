---
layout: post
title: "Test of code"
date: 2014-04-01 21:33:09 -0400
comments: true
categories: 
---
JSON is one of the major data formats out there on the web, known for its readability. Personally, I was a little unsure about that readability aspect after pulling up my first JSON document and seeing this mess.

![Crazy JSON!](http://gdurl.com/PP1x) 
 
The first step towards wrapping your head around JSON is to see it printed in a prettier fashion. Head over to [JSON Online Editor](http://www.jsoneditoronline.org) and using the "Open URL" option you can paste the URL to a JSON document and see this format is actually much more presentable than it lets on. (If you need a JSON example to play with while reading this, don't hesitate to use [my Treehouse profile](http://teamtreehouse.com/johnkeith.json), as this provides you with a complex, multidimensional set of data to manipulate).

I decided to start by figuring out how to work with JSON in Ruby, as currently I feel more comfortable with Ruby than Javascript. Luckily, Ruby makes handling JSON from the web easy with a few of its built in libraries and modules.

At the top of your Ruby file (or in IRB if you would rather try this out in the terminal), you will need to require the Net/HTTP library and the JSON module.

``` ruby
require 'net/http'
require 'json'
```

Net/HTTP allows you to do all types connect to websites within Ruby and do all types of nifty stuff. For instance, the following code will assign our JSON document's contents to the variable response. 

``` ruby
response = Net::HTTP.get_response(URI.parse('http://teamtreehouse.com/johnkeith.json'))
```

The get_response method returns a Net::HTTPResponse object that contains header and body information from the website specified. Since we are are specifying a JSON document, there is no header, but you can check the output of your response object with `response.body.inspect`.

Now that we have the JSON document retreived from the web, we need to parse it and turn the data into something more easily used by Ruby.

``` ruby
result = JSON.parse(response.body)
```

(I found it helpful to look at the difference between the raw Net::HTTP response and the parse JSON - try running `puts JSON.pretty_generate(result)` and `puts response.body` to see how the parse method formats the data into a Ruby readable hash.) 

Next, we need to access the data within our newly parsed hash of JSON data. You can access Ruby hashes with a similar syntax to the one used for arrays - start with the hash name, then a key from the hash in brackets. 

``` ruby
result["badges"]
result["badges"][0]
result["badges"][0]["name"]
```

The examples above show you how you can move through a nested hash and access data within different sections of your JSON document. Putting this syntax to use, you can quickly pull out all the URLs for the badge icons from this Treehouse JSON. 

```
result["badges"].each do |item|
  puts item["icon_url"]
end
```

While I thought it was awesome to be able to drill down to these URLs, I decided I wanted to do something with this data. To round out my exploration of JSON and Ruby, I wrote a small script to grab all of the images located at these URLs and save them to my computer. 

```

require 'open-uri'
result["badges"].each do |item|
  open("badge#{item["id"]}.png", "w+") do |file|
    open(item["icon_url"]) do |image|
      file.write(image.read)
    end
  end
end
```

The Open URI module, according to the Ruby docs, allows you "to open an http, https, or ftp URL as though it were a file." The code above uses this capability in the `open(item["icon_url"] do |image|` line in order to open the URL we extracted from the hash and then save that image data into a file.
