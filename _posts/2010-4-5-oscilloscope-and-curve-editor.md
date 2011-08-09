We've made some big steps lately so I figured it was time for a short update.
Fabian's great work on the native bindings for the SuperCollider synthesis
server now allow us to boot the audio server in the same process as the JVM.
This means we can share buffers of audio data with the DSP engine with minimal
communications overhead, allowing for real-time visualization and soon
manipulation of audio waveform data.  

The new (oscillo-)scope renders the contents of a buffer.  It can animate in
real-time with an adjustable fps, but their is no zooming or waveform
manipulation yet.  It's already usable for checking out waveforms and learning,
but hopefully there are still some good opportunities for optimizing this widget
to get a bit cleaner, real-time waveform without jitter.  (I haven't tried out
either the concurrent garbage collector or the real-time JVM, both of which
could be interesting.)

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

Shown in the oscilloscope is a kick drum sample.

<a class="fancy" href="media/new-curve-editor-big.png">
  <img src="media/new-curve-editor-small.png"/>
</a>

Below the oscilloscope is the new curve editor.  This is the result of a late
night hacking session last night, so there is plenty more work to do, but this
will allow us to visualize and manipulate the control points for envelope and
automation curves.

The color chooser in the toolbar on the side emits a **:color-changed** event when the color is
changed.  For most stuff you can probably just use the **live-color** function
though.  Here's how you can change the color of the curve editor interactively:

{% highlight clojure %}

  (live-color #(curve-color %))
  ;... change color ...
  (stop-color)                       ; remove the handler
{% endhighlight %}

I've been thinking about how to generate a little theme configuration panel that
lets you see all of the colors used by the application, adjust them
interactively, and then save out into a named theme setting.  This will be one
of the building blocks.

Our goal for this first draft of an actual Overtone application is to create a
tool that is good for designing and playing a single instrument.  This includes
a basic live-coding editor, a repl, the oscilloscope, the curve editor, and a few
generic controls to trigger synths and control parameters.  Oh, and some basic
midi hooks to make it easy to use a keyboard or a monome to trigger synths.  We
are probably a month or two away from the first alpha release.
