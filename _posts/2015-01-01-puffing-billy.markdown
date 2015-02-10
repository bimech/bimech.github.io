---
layout: post
title:  "Simplify your acceptance testing environment with puffing-billy"
date:   2015-01-01 20:37:00
categories: development 
author: Frank O'Hara
---
Automated browser-based acceptance testing is a valuable but costly undertaking.  There are costs associated with execution time, test maintenance and environment configuration.  If the application under test also happens to have a service oriented architecture, the costs of test-environment configuration can multiply. Lately, I’ve started using [puffing-billy](https://github.com/oesmith/puffing-billy) to reduce the number of dependencies needed to run automated acceptance tests.

If you’re familiar with tools like [VCR](https://github.com/vcr/vcr), you’ll catch on to puffing-billy quickly.  By it’s own estimation, VCR enables you to “Record your test suite’s HTTP interactions and replay them during future test runs for fast, deterministic, accurate tests.”  Indeed, VCR allows you to mock HTTP requests to eliminate a test’s dependance on external resources.  This allows your tests to run faster, and you always retain the ability to disable mocking when you want to exercise the integration of services.

Puffing-billy [now provides](http://swizec.com/blog/bring-ruby-vcr-to-javascript-testing-with-capybara-and-puffing-billy) similar HTTP mocking functionality.  It sits between the browser and the web app server and acts as a proxy.  When an HTTP request is made to the web app server during an automation session, puffing-billy intercepts the request and can return a mock response if you tell it to.  Similar to VCR, this mocked response is essentially a cached response of a previous HTTP interaction, so the client consuming the mock is none the wiser.

This mocking ability is particularly useful when running browser-based acceptance tests against an SOA.  For instance, let’s say the client-side app makes an AJAX request to the public server-side app for a JSON object. To construct that object, the public server might in turn have to talk to one or more private services. So, to get this test running in a continuous integration environment such as [Jenkins](http://jenkins-ci.org/), you must have the full stack of every service dependency up and running.  That’s a lot of configuration and maintenance for just responding to the client with some JSON.

Instead of getting your entire architecture chugging when you want to run a few Capybara specs, just have puffing-billy serve up cached responses of previous HTTP interactions.  With this approach, your acceptance tests can run in CI without having numerous backend services on-line.  All client-side requests can be satisfied by the puffing-billy proxy.  Just as with VCR, when you want to do full-stack integration testing just disable the proxy and your acceptance tests magically become indirect integration tests.

I contributed to a puffing-billy [pull request](https://github.com/oesmith/puffing-billy/pull/30) that was recently merged in which adds some enhancements for using the tool with an SOA, and I’m excited to have this in my toolbox. As more and more web apps continue to beef up their client-side, it’s a great opportunity to find ways to simplify acceptance testing of those clients.