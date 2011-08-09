This post is about the inst branch of Overtone that I'm working on.  The goal is
to split up some of the functionality of the currenty synth and defsynth
functions.  Instead we will have a low-level synth interface, and a higher level
instrument interface.  Instruments are automatically added to the session when
they are defined, and they will return back a player function.  Calling an
instrument function triggers the underlying synth.  

* synthdef 
 - create raw synthdef object

* synth 
 - macro to let-bind operators to ugen functions
 - anonymous if no name symbol present
 - auto-load onto synth server
 - return callable map with sdef and trigger function
 - by default all synths play in the SYNTH-GROUP

* defsynth
 - (def foo (synth ...))

* play
 - uses synth underneath, loads and triggers immediately when ready

* inst (rument)
 - calls synth to define and load the synth
 - register itself with current session
 - creates a group to contain synth instance nodes
 - automatically adds pan and output ugens with existing rules

* definst 
 - (def foo (inst ...))

{% highlight clojure %}

  ; View a full sample waveform
  (def s (load-sample "/home/rosejn/studio/samples/kit/boom.wav"))
  (scope-buf s)

  ; view a live waveform
  (def b (buffer 2048))
  (defsynth foo [out-bus 20] (out out-bus (sin-osc 400)))
  (foo)           ; output a sine wave onto bus 20
  (bus->buf 20 b) ; record signal from bus 20 into buffer b, looping
  (scope-buf b)   
  (scope-on)      ; enjoy
  ;...
  (scope-off)     ; stop live updates

{% endhighlight %}

