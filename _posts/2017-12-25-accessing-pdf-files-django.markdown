---
layout: post
title: "Accessing PDF files in Django"
date: 2017-12-25 12:20:29 +0530
categories: django
---

As can be cited from Django website, Django uses request and response objects to pass state through the system. When a page is requested, Django creates an `HttpRequest` object that contains metadata about the request. Then Django loads the appropriate view, passing the `HttpRequest` as the first argument to the view function. Each view is responsible for returning an `HttpResponse` object.

Following along these lines to provide access to our pdf file such as *resume*, we first need to add the url pattern in `apps/url.py` to access our file.

`url(r'^xyz/$', views.xyz, name = 'xyz')`

Then add the view function passed in `apps/view.py` as follows.

{% highlight python %}
def xyz(request):
    file = open('path/to/file/to/display', 'rb')
    response = HttpResponse(file, content_type='application/pdf')
    return response
{% endhighlight %}
Firstly, we need to open the file by defining the path to it, and then define the content type while getting the `HttpResponse`. Also unlike `HttpRequest` which is handled automatically by Django, `HttpResponse` needs to be handled by the programmer.

Note that, it's always a good practice to close the file opened due to various reasons. However, since we are only reading and not writing the file, its OK not to close it, python will garbage collect it later. Be careful if you are using it to open many files using a loop, you may end up with a problem of lack of file descriptors and may encounter an error.      