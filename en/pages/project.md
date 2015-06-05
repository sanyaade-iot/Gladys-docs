Gladys is an home automation assistant to help you in your everyday life.

Yes, like a kind of JARVIS!

When you see this kind of project, you say "Uhh, I'm sure this don't work, it's based on speech recognition, even Siri isn't capable of being JARVIS". But the goal of Gladys project is **completely different**. We believe that speech recognition is not working fine today, so we've tried a different approach : If instead of having an assistant waiting for your orders, we have an assistant analyzing all your environment ( analyzing your calendar, reading your emails ) and **predicting your needs**. Because in fact, with all the APIs which exists, we can gather all the information we want to optimize our life.

With this system, it's not the user who ask something to his assistant : it's the assistant which tells informations to the user, **at the right moment**.

Interested in Gladys ? [Try it at home](/en/installation), it's free !

Don't hesitate to share the project, if we want Gladys to be as good as possible, we need your help. The more we are on the project, the better it can be !

<div class="row">
            <ul class="list-inline list-share-gladys">
                <li>
                    <a href="https://twitter.com/gladysproject" class="twitter-follow-button" data-show-count="false">Follow @gladysproject</a>
                    <script>!function(d,s,id){var js,fjs=d.getElementsByTagName(s)[0],p=/^http:/.test(d.location)?'http':'https';if(!d.getElementById(id)){js=d.createElement(s);js.id=id;js.src=p+'://platform.twitter.com/widgets.js';fjs.parentNode.insertBefore(js,fjs);}}(document, 'script', 'twitter-wjs');</script></li>
                <li>
                    <a href="https://twitter.com/share" class="twitter-share-button" data-text="Meet Gladys, your home automation assistant !" data-via="gladysproject" data-count="none">Tweet</a>
                    <script>!function(d,s,id){var js,fjs=d.getElementsByTagName(s)[0],p=/^http:/.test(d.location)?'http':'https';if(!d.getElementById(id)){js=d.createElement(s);js.id=id;js.src=p+'://platform.twitter.com/widgets.js';fjs.parentNode.insertBefore(js,fjs);}}(document, 'script', 'twitter-wjs');</script>
                </li>
                                <li>
                    <a class="gh-btn" id="gh-btn" href="https://github.com/GladysProject/Gladys" target="_blank"><span class="fa fa-github fa-lg"></span> Fork</a>
                </li>
                <li>
                    <a class="gh-btn" id="gh-btn" href="https://github.com/GladysProject/Gladys" target="_blank"><span class="fa fa-github fa-lg"></span> Star</a>
                </li>
            </ul>
        </div>



## Hardware

Gladys is written in full Node.js, so it works in any systems: Linux, Mac, Windows. ( and even on a server, dedicated or VPS !)
But for more home automation interaction, you should use a Raspberry Pi.

The followings hardwares points are my installation, but you can build your own, Gladys is not built to be only compatible with theses devices.

### Raspberry Pi

Why Gladys on a Raspberry Pi ?

* Price : almost 30$ for a Raspberry Pi 2.
* A Raspberry Pi can be on 24/7, without making any noises.
* Power consumption is very low.
* With GPIO ports, home automation possibilities are infinite!
 
###Arduino

A Raspberry Pi is good for executing some strong code, but for little electronics interaction, nothing is better than a arduino.

I've connected an Arduino in USB to my Raspberry Pi to receive 433Mhz signals.

###Remote control plug

To control lamps, coffee machine, we can use 433Mhz plug to control them wirelessly.

###Sensors

To know when someone is coming one, we can use 433Mhz motion sensors, and receive the signal with our Arduino.

###Lights

We can control the light with connected light bulb, like Philips Hue, or chinese equivalent.

## The Software

Gladys is written in 100% Node.js, with server-side [Sails.js](http://sailsjs.org/), and client-side [AngularJS](https://angularjs.org/).

<img src="/assets/images/pages/project/gladys_schema.jpg" class="img-responsive medium-image"/>

Gladys is available on [Github](https://github.com/GladysProject/Gladys), you can download it for free :)

