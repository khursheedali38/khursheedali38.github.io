---
layout: post
title: "Deploying Django Webapp"
date: 2018-01-14 18:07:39 +0530
categories: django
---

I could sense feeling of accomplishment after my final build of personal website on my development server, only to realize that deploying on production server isn't that straight forward. In fact, Digital Ocean's One Click App makes things easy for you, but you still have to take care of some stuff. You could encounter several issues and may find it hard to circumvent them, so herein I try to compile all the issues and their solutions.

Firstly, for those using [django_markdown][django-md] for html rendering, you won't be able to see the preview of your markdown written in the admin console, this is because the underlying view function is using deprecated `POST` request construct. That is, `requests.REQUEST` is deprecated and you need to replace it with `request.POST`.

Therefore, Head on to `django_markdown` directory found in `.../dist-packages` on our production server and open `views.py`. And do as follows:

{% highlight python %}
#content=request.REQUEST.get('data', 'No content posted') 
content=request.POST.get('data', 'No content posted')
{% endhighlight %}

Another issue pertaining to `django_markdown` is that you might see the warning related to `url.patterns()`. Again this is deprecated, and needs to be fixed, so move to `.../dist-packages` and change `urls.py` as follows.

{% highlight python %}
""" Define preview URL. """

from django.conf.urls import url

from .views import preview

urlpatterns = [
    url('preview/$', preview, name='django_markdown_preview'),
    ]
{% endhighlight %}

Secondly, once you have transferred required apps on production server and installed them, make sure to go ahead edit the `settings.py` file on your production server found at `django/django_project/django_project` by making the following changes :

{% highlight python %}
DEBUG = False
ALLOWED_HOSTS = ['example.com']
ALLOWED_HOSTS += ipaddresses()
{% endhighlight %}

To know more on these, head on to [Settings documentation][settings-doc] and [Deployment checklist][doc-check].

Lastly, you may encounter `Server Error (500)` when accessing `/admin`, which is mainly because the database is in read mode. If you clicked and dragged the sqlite database via WinSCP or another similar funtionality, this means it was created by the `root` user, so you will need to give read/write access to the sqlite file. You can give the django user (on your server) permissions to write to the database file by doing something like this on your production server console `chown django:django db.sqlite3`.

[django-md]: https://github.com/klen/django_markdown
[settings-doc]: https://docs.djangoproject.com/en/2.0/ref/settings/#std:setting-ALLOWED_HOSTS
[doc-check]: https://docs.djangoproject.com/en/2.0/howto/deployment/checklist/