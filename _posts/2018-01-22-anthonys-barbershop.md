---
layout: post
title:  "Anthony's Barbershop"
date:   2018-01-22
author: Seth Furman
categories: web progamming javascript html css golang api s3
---

<style>
    @import url("https://fonts.googleapis.com/css?family=Lobster+Two");
    h1, h2, h3 { font-family: 'Lobster Two'; }
</style>

## Creating a webpage
During my winter break (Dec. 2017 to Jan. 2018) I decided to create a webpage
from scratch to brush up on HTML, CSS, and JavaScript and to practice creating
a simple web API to dynamically update the webpage using Ajax.

I took inspiration from the [webpage of my local
barber](http://www.langhornebarber.com/), Anthony Canamucio, and created a new
webpage based off of the style of his barbershop: green paneling, neon signs,
and retro fonts among other accents.

## The '/hours' API
On top of the static page, I wanted to create a RESTful `/hours` microservice
so the page could easily fetch business hours in the background. A privileged
user could then add or delete hours objects with a user-friendly front-end,
without someone having to manually update the HTML for every holiday or
temporary change in regular hours.

### The server
I implemented this service using the [Gin](https://gin-gonic.github.io/gin/)
framework for golang.

...Swagger doc.

### Users
### Authentication
### Authorization.

## The front-end to the API

## The Webpage
Click [here](/assets/documents/anthonys-barbershop/home.html) for the
stand-alone webpage.
<iframe style="width: 90%; height: 50vw" src="/assets/documents/anthonys-barbershop/home.html"></iframe>
