---
layout: post
title:  "Make your tests resilient to browser focus"
date:   2015-01-10 20:37:00
categories: Test Automation
author: Frank O'Hara
---
Focus-related test failures can be tricky to diagnose.  One moment your tests pass, the next moment they fail.  Same code, same data, no race conditions or timing issues, and yet intermittent failures crop up.  I encountered this recently while tweaking a test suite to support [Capybara-Webkit](https://github.com/thoughtbot/capybara-webkit), which is a headless Webkit driver for [Capybara](https://github.com/jnicklas/capybara).  Previously, we had only been using the [Selenium](http://docs.seleniumhq.org/) driver and we wanted to add support for both local and remote headless execution.

After I had ironed out all of the configuration related issues, I noticed that tests executed with headless Webkit were not intermittently failing, as they were with Selenium.  At that point I realized this was almost certainly a focus-related issue, as a Selenium-controlled browser is much more susceptible to losing focus than a headless browser.  Sure enough, when I dug into the code I noticed that we had a web form with input elements that were dependent on blur events firing to complete their business logic.  Without browser window focus, Selenium cannot conventionally trigger blur events, and tests start behaving strangely.

It was especially difficult to diagnose the blur issues with the test I was working on because visibly (and network-wise) the test appeared to be doing what it was supposed to do.  The text inputs were populated with the correct data, the submit button was pressed and an AJAX request was made to the server.  The response from the server, however, was incorrect.  Digging into the code further, I noticed the blur event handlers were designed to incrementally augment the AJAX request.  As the events were never getting triggered, the request was never augmented and instead a default request was made, which of course returned a different response.

The solution ended up being somewhat heavy-handed, but necessary: trigger the events manually with JavaScript.  So where previously I was doing something similar to:

{% highlight ruby %}
fill_in "Foo", :with => "bar"
{% endhighlight %}

I was now doing:

{% highlight ruby %}
fill_in "Foo", :with => "bar"
page.execute_script("$('#foo').blur()")
{% endhighlight %}

I was also using the excellent [SitePrism](https://github.com/natritmeyer/site_prism) page object library, so I was able to wrap those two steps in a simple method.  It was a small change that made all the difference; tests now ran reliably whether the browser had focus or not.  I view this solution as a fight-fire-with-fire approach.  Injecting JavaScript into an automation sessions isn’t really a legitimate representation of user interaction, but it is also not possible for a user to enter text when the browser does not have focus, but Selenium merrily does so anyway.  If Selenium is going to bend the rules of user interaction, you shouldn’t feel bad about bending them back to get your tests back into a stable state.

