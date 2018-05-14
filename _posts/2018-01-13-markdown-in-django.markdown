---
layout: post
title: "Markdown in Django - GitHub API"
date: 2018-01-13 16:35:39 +0530
categories: django
---

Supporting markdown in Django is a commonly discussed issue after the python package for django,  `django.contrib.markup` was deprecated. Many applications such as, [django_markdown][django-md], extend the support to markdown in Django and have a very active developer community. 

But amid these applications, there exists [GitHub API][github-api] which provides GitHub flavored markdown. To use GitHub API for markdown, HTML rendering you first need to Authenticate your application requests. There are three ways to authenticate your requests through GitHub API v3 :

+ OAuth2 Token (Header)
+ OAuth2 Token (Parameter)
+ Basic Authentication

The advantage of authentication is that you can make up to 5000 requests per hour, as compared to unauthenticated requests where the rate limit allows for up to 60 requests per hour. Follow the [GitHub API][github-auth] for authentication.

Once we are done with that, we need to make `POST` requests to send our markdown string/data using the GitHub API. Also, GitHub API accepts data in `JSON` string format, so we need to ensure that aswell. We define a views function in `apps/view.py` to make requests and get responses from the API as follows.

{% highlight python %}
import requests
import json
from app.models import MyModel

data_list = MyModel.objects.values_list('text', flat=True) 
for text in data_list:
    data = { "text": text } 
    response = requests.post("https://api.github.com/markdown", json.dumps(data))
    data_list.update(text=response.text)
{% endhighlight %}

Assume that we would like to translate markdown field in our model into HTML to render. Firstly, we get the objects and filter it to get the text column. Note that objects values are returned as tuple, use `flat=True` parameter to return as single value. Secondly, iterate over each text value and convert it into `JSON` string using `json.dumps()`. Finally, update the text content.

[django-md]: https://github.com/klen/django_markdown
[github-api]: https://developer.github.com/v3/markdown/
[github-auth]: https://developer.github.com/v3/#authentication