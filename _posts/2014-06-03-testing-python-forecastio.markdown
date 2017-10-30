---
layout: post
title: Testing Python-Forecastio
date: '2014-06-03 15:23:20'
tags:
- python
- testing
- thoughts
---

One of my more popular open source projects is a Python weather forecasting package called [Python-Forecastio](https://github.com/zeevg/python-forcast.io).

The project wraps the [Forecast.io](http://forecast.io) JSON API in a Python interface. This provides an intuitive way to interact with the weather service.

Recently I have started testing the package on [Travis](https://travis-ci.org/).  This is the first project which I have used Travis for testing, normally using [CircleCI](https://circleci.com/) where open source transparency is not a concern.

My first impressions are quite good.  You define your build configuration in a YAML file which should be placed in the root of your repo.

Here is mine.
{% highlight yaml %}
language: python

python:
  - "3.3"
  - "2.7"

install:
  - "pip install -r requirements-test.txt"

script: nosetests --with-coverage

after_success: coveralls
{% endhighlight %}
    
    
The file specifies that the tests should be run against both Python 2.7 and 3.3.  Testing both versions of Python also ensures cross compatibility.

The next step is to push a commit to your GitHub repo.  Travis picks up the commit and runs the `script` command specified in the YAML file.

This can be a fairly slow process, it took around 15mins after pushing before I actually had the results. Especially when I'm used to the very quick turn around time of [CircleCI](https://circleci.com).

Still, if your project is public, Travis will run your tests for free and this is a *really* good thing.  Writing tests should be encoraged by the open source community because it sets a good example for novice developers and provides assurance to its user base. Travis is supporting this idea by making testing services more accessible.

If you want to take a look at my projects latest test results, they can be found [here.](https://travis-ci.org/ZeevG/python-forcast.io)