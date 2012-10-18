===================================
Pyramid on OpenShift using Buildout
===================================

This repository contains a buildout-based deployment template for Pyramid web
framework. This template have been configured to work with your existing
pyramid project eggs which was created using the pcreate command. Check
`site.cfg.sample` on how to load your project into this template. 

Running on OpenShift
=====================

Create an account at http://openshift.redhat.com/

Create a DIY application::
  
  rhc app create -a myapp -t python-2.6

Add this upstream Plone repo::
  
  cd myapp
  git remote add upstream -m master git@github.com:kagesenshi/pyramid-buildout-openshift-quickstart
  git pull -s recursive -X theirs upstream master

Copy `site.cfg.sample` as `site.cfg` and edit it to configure::

  cp site.cfg.sample site.cfg

Commit `site.cfg`::

  git add site.cfg
  git commit

Then push the repo to OpenShift (this will take quite a while to finish)::
  
  git push

Thats it, you now can check out your application at::

  http://myapp-$yournamespace.rhcloud.com

Notes
======

Caveat
------

You will have to use different name for your static directory as OpenShift maps
`/static` url to `$OPENSHIFT_REPO_DIR/wsgi/static` causing static urls to 
break. For example, let rename it to `resources`. In `__init__.py`, change::

  config.add_static_view('static', 'static', cache_max_age=3600)

to::

  config.add_static_view('resources', 'static', cache_max_age=3600)

