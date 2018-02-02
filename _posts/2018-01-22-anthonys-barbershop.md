---
layout: post
title:  "Anthony's Barber Shop"
date:   2018-01-22
author: Seth Furman
categories: web progamming
---

<style>
    @import url("https://fonts.googleapis.com/css?family=Lobster+Two");
    h1, h2, h3, h4 { font-family: 'Lobster Two'; }
</style>

## A webpage
During my winter break (Dec. 2017 to Jan. 2018) I decided to create a webpage
from scratch to brush up on my HTML, CSS, and JavaScript and to practice
creating a simple web API to dynamically update the page using Ajax.

I took inspiration from the [page of my local
barber](http://www.langhornebarber.com/), Anthony Canamucio, and created a new
site based off of the style of his barbershop: green paneling, neon signs,
and retro fonts among other accents.

## "/hours" API
On top of the static page, I wanted to create a RESTful `/hours` API
so the page could fetch business hours in the background. A privileged user
could then add or delete 'hours set' objects with a user-friendly front-end,
without someone having to manually update the HTML for every holiday or
temporary change in regular hours.

### Implementation
I implemented [my service](https://github.com/sfurman3/anthonys-barbershop-api/tree/release_v1)
using the [Gin](https://gin-gonic.github.io/gin/) framework for golang and
hosted it on a [DigitalOcean droplet](https://www.digitalocean.com/products/droplets/).

Business hours are represented and stored as JSON blobs on the server. When the
homepage loads, the latest hours are fetched, converted into 0 or more HTML
tables, and inserted into the document.

As of now, the following methods are supported and enabled:
- GET: `/hours`
- GET: `/hours/findActive`
- GET: `/hours/findByName/:name`

#### Try it out
Enter one of the paths above into the text box below (e.g.
<code>/hours/findByName/regular</code>).

<code>
GET: <input id="api-get-input" type="text" value="/hours">
</code>
<pre id="api-response">
{}
</pre>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
<script>
var apiBaseUrl = "https://bigturtle.me";

function getRequest(path) {
    var httpRequest = new XMLHttpRequest();
    httpRequest.onreadystatechange = function() {
        if (httpRequest.readyState === XMLHttpRequest.DONE) {
            if (httpRequest.status === 200) {
                var resp = JSON.parse(httpRequest.responseText);
                $("#api-response").text(JSON.stringify(resp, undefined, 2));
            } else {
                try {
                    var resp = JSON.parse(httpRequest.responseText);
                    $("#api-response").text(JSON.stringify(resp, undefined, 2));
                } catch (err) {
                    $("#api-response").text(httpRequest.responseText);
                }
            }
        }
    };
    httpRequest.open('GET', apiBaseUrl + path, true);
    httpRequest.send();
}

$("#api-get-input").keyup(function(event) {
    if (event.keyCode === 13) {
        var path = document.getElementById("api-get-input").value;
        getRequest(path);
    }
});
</script>

<span style="color: #e8437c; font-size: 1.2em; font-family: 'Lobster Two'">Note:</span> The PUT and DELETE methods (for adding
and removing sets of business hours) are implemented but disabled since neither
endpoint currently supports authentication and I have yet to create a
user-friendly front-end.

## The Webpage
Click [here](/assets/documents/anthonys-barbershop/home.html) to view the
stand-alone webpage.

Business hours are populated in the "When we do it" section at the bottom of
the homepage.

<iframe style="width: 90%; height: 50vw" src="/assets/documents/anthonys-barbershop/home.html"></iframe>

## Quick links
- [Mr. Canamucio's original webpage](http://www.langhornebarber.com/)
- [My version of the barbershop webpage](https://github.com/sfurman3/anthonys-barbershop-webpage)
- [Source code for the `/hours` API](https://github.com/sfurman3/anthonys-barbershop-api/tree/release_v1)
- [Source code for this webpage](https://github.com/sethfurman/sethfurman.github.io/blob/master/_posts/2018-01-22-anthonys-barbershop.md)
