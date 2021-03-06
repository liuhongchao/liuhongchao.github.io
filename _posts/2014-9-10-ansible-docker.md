---
layout: post
tags: Ansible
category: Software
hide_in_overview: true
title: Provision Docker using Ansible
---

I love [Ansible](http://www.ansible.com/) and
[Docker](http://www.docker.com), they are great two pieces of
software that work pretty nicely together. While there is [ansible
module](http://docs.ansible.com/docker_module.html) to manage docker
containers, docker images themselves can be built using ansbile as
well. We just need a base images that's ansible enabled to start with:

{% highlight dockerfile linenos=table %}
FROM phusion/baseimage:0.9.11
MAINTAINER HC

# Bootstrap Ansible
RUN apt-get -y update
RUN apt-get install -y python-yaml python-jinja2 git
RUN git clone http://github.com/ansible/ansible.git /tmp/ansible
WORKDIR /tmp/ansible
ENV PATH /tmp/ansible/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV ANSIBLE_LIBRARY /tmp/ansible/library
ENV PYTHONPATH /tmp/ansible/lib:$PYTHON_PATH

EXPOSE 22 3000
{% endhighlight %}

