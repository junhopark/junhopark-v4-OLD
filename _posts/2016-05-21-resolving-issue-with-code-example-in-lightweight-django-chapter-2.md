---
layout: posts
---

I've been reading through the book 'Lightweight Django' by Julia Elman and Mark Lavin and I was having a lot of trouble getting the final example in Chapter 2 to work.  The local server would start up but when going to http://localhost:8000 I would encounter the following error:

    RuntimeError at /
    Model class django.contrib.contenttypes.models.ContentType doesn't declare an explicit app_label and isn't in an application in INSTALLED_APPS.

I tried debugging it myself & tried Googling around for a solution for quite some time.  Finally, after trying & trying again I came across a solution that worked.  I added 'django.contrib.contenttypes' and 'django.contrib.auth' to the INSTALLED_APPS section in placeholder.py (in addition to 'django.contrib.staticfiles' which was already present).  Like this:

    ...
    INSTALLED_APPS=(
        'django.contrib.staticfiles',
        'django.contrib.contenttypes',
        'django.contrib.auth',
    ),
    ...

I'm running Python 3.4.4 + Django 1.9.6 while the examples in the book were tested with Python 3.3 & 3.4 and Django 1.7.  I'm guessing this has something to do with why the examples in the book did not work as expected.

Hope this might be helpful to Django newbies who are reading through the book.  By the way, it's been an excellent book so far with solid examples.  Looking forward to reading the rest of it.
