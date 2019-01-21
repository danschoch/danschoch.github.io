---
layout: post
title:      "AJAX Basics Using jQuery"
date:       2019-01-21 18:26:56 +0000
permalink:  ajax_basics_using_jquery
---

Recently, I started my journey into Javascript. While JS is useful (indispensible, really) for many different reasons, one of the first that I've come across is the AJAX request. Below are some thoughts for the uninitiated from the point of view of the slightly more initiated.

## Why Ajax?
If you've started learning web development, you'll likely have come across the basics of how modern web apps function. In a nutshell, a person connected internet uses their web browser to send a request for information (e.g. a page on a website) and the server that corresponds to the domain that the request was made to returns that information and/or makes changes to any data that needs to be changed per the request. This is the client-server model that the web is based on. Traditionally, any modification to a page on a web client after this request would require a complete refresh of that page to show any updated information that the server sent back. Javascript and AJAX technique changed that. 

AJAX stands for Asynchronous Javascript and XML (for brevity, I'm going to skip over the XML part... it's a remnant from when the technology emerged that's no longer very relevant). AJAX is a technique that allows for a client and server to communicate without refreshing the current page in the client. For instance, a blog post comment can be sent to a server, the database can be updated, and the post can be displayed below the post somewhere, all without a full refresh. AJAX is used all over the web, from Twiiter, to Google, and everywhere in between. It provides a much faster, less jarring experience to users than traditional full page refreshes coming from the server. One of the main reasons for this is that "asynchronous" means that these requests are non-blocking and completed in the background. That is, once the user makes their request, the rest of the code on the web page continues to execute while the request is made behind the scenes. Once the request is fulfilled (or there is an error returned), that data updates in DOM without the page refresh.

## jQuery and AJAX
AJAX requests are completely feasible in vanilla JS, but I'll focus on how to use jQuery to make these requests, since it is considerably easier to understand the basic protocol this way, in my opinion. I'll go over a  basic GET request, although you can use jQuery to do other types of HTTP requests as well.

In this example, we'll be talking about a fake blog application with the domain "www.blogsite.com". The idea is that you have the ability to create blog posts, comment on them, etc. Nothing fancy here. AJAX requests generally go to an API of some sort that returns data in a JSON format. If you're unsure of what those terms mean, I'd suggest a basic google search to understand them before moving on.

Let's say you want to render a list of comments underneath a blog post. (For the sake of this example, the URI below returns a JSON array with only the comments associated to the post the client is currently viewing.) That would be an HTTP GET request, and would look something like this in jQuery:

```
<html>
  <body>
	
	  <div>
      <ol id='commentList'>
      </ol>
    </div>
	
	
  </body>
</html>


<script type="text/javascript">
$( document ).ready(function () {
  $.get("http://www.blogsite.com/comments", (data) => {
    data.forEach(comment => {
        
      $("#commentList").append(
        `<li>${comment.content}<br>
        Posted By: ${comment.author}</li>`
      );

    });
  });
}
</script>

```

The HTML at the top of the code is simply an example to demonstrate where we might place this data upon it's successful request. It could, for instance, be placed below the main body of the sample blog post.

The AJAX magic is all happening in the script tag below the HTML. The first line tells the client to load the following code once the DOM is properly loaded in the client. The second line uses the jQuery function .get() to initiate the asynchronous GET request. Two arguments are provided to the function. First, the URI where we can find the data we are looking for. The second argument is a callback function that will execute once the request is completed. The data returned from that request is passed in as an argument. In this example, that data is a list of JS objects that each represent a comment on the blog post. So, we use the .forEach() method to iterate over each of these JS objects. In each case, we use a jQuery selector to select the ordered list with the ID "commentList" and append a new list item that includes the comments content and author. That data comes from the current JS object that the iteration is on. This process repeats until all the JS objects returned from the GET request have been iterated over, and, voila, you have a list of comments rendered below the blog post.

## Moving Forward
I have a lot more to learn about Javascript in general, and asychronous Javascript in particular. This type of technique really is foundationtal to modern web applications (single-page applications, etc.), so even though the journey to proficiencey in front-end development is just starting for me, it's exciting to have a bit of the basics covered. Hope this is a help to anyone in a similar situation.
