===================================
Pyramid on OpenShift using Buildout
===================================

This repository contains a buildout-based deployment template for Pyramid web
framework

Running on OpenShift
=====================

Create an account at http://openshift.redhat.com/

Create a DIY application::
  
  rhc app create -a myapp -t python-2.6

Add this upstream Plone repo::
  
  cd myapp
  git remote add upstream -m master git@github.com:kagesenshi/pyramid-buildout-openshift-quickstart
  git pull -s recursive -X theirs upstream master

Then push the repo to OpenShift (this will take quite a while to finish)::
  
  git push

Thats it, you now can check out your application at::

  http://myapp-$yournamespace.rhcloud.com

Notes
======
