The audio synthesis API that communicates with SuperCollider is operational.
You can define a synthesizer, load it and then trigger it and send it control
messages to adjust parameters.  Here's a short example of creating and playing a
simple synth on the repl.

{% highlight clojure %}

(use 'overtone.live)

; import the UGen function library
; we do it this way because we need to override a bunch of built-in clojure
; functions, including +, -, *, / and other common functions.  Doing it like
; this saves you from having to exclude all this in your namespace definition.
(refer-ugens)

; boot the synth server
(boot)

; here is a random, echoing, ping synth
(defsynth chop-saw [freq 440 depth 5]                                                                                     
  (comb-n (* (env-gen (perc 0.1 0.4) (lf-pulse:kr 2)) 
             (rlpf (saw (+ freq (* depth 
                                (lf-saw:kr (lf-pulse:kr 0.1 0.2))))) 
                   freq 0.6))))

; play it
(chop-saw)

; kill the synth instance based on the last returned node id
(kill *1) 

; play it with different settings
(chop-saw 440 20)

; and control them on the fly
(chop-saw :ctl :freq 880 :depth 10)

; make some more
(chop-saw :freq 440)
(chop-saw :freq 220)
(chop-saw :freq 110)

; clear all running synths
(reset)

; quit the synth server
(quit)

{% endhighlight %}

A graph based editor (connecting nodes with edges) is coming to life now.  This
will allow you to define synthesizers and control patches in a basic graphical
programming environment.  Here's a screenshot showing some of the widgets
implemented in the first prototype (click to zoom):

<a class="fancy" href="media/overflow.png"><img src="media/overflow-small.png"/></a>

Overtone can be used as a library from Clojure code or on the repl, but there is
also the beginnings of a standalone application.  It currently boots the server
and it has a repl that can evaluate code, but it will soon get a text editor and
the flow editor.

