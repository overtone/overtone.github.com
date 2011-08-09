---
layout: default
title: Overtone
---

## Roadmap ##

* Live-code editor

  A text editor ala [processing](http://processing.org) tuned for live-coding and
  synth design.
  
  - [scenegraph](https://scenegraph.dev.java.net/)
  - [jvi](http://jvi.sourceforge.net/)
  - [jsyntax-pane](http://code.google.com/p/jsyntaxpane/)

* overflow node editor
  
  A visual programming surface similar to Max/MSP or PD.  You connect processing
nodes in a data-flow graph to design SuperCollider synths and instrument
controllers.  Synths designed in Clojure code can also be visualized on the
surface.

  - [netbeans visual](http://platform.netbeans.org/graph/)

* diagnostic panel

  A basic status panel showing the processing rate, cpu usage, connectivity to
audio servers, network usage, etc...

  - [scenegraph](https://scenegraph.dev.java.net/)
  - swing

* jackd auto-start and connect in linux

  Do whatever is necessary to automatically connect with jack when using linux. 

  - [clojure-jna](http://github.com/Chouser/clojure-jna)

* include libscsynth in jar file and boot server in process

  Link directly with the SuperCollider library and start the server in the same
process as the JVM so we can have lower latency osc communication, and direct access to buffers of audio data for real-time visualization.

  - [clojure-jna](http://github.com/Chouser/clojure-jna)
  - [SuperCollider](http://supercollider.sourceforge.net/)

* synth browser

  Start with a simple Swing tree browser to select synths in your local
collection.  Later develop a custom browser widget on top of a graph database
that integrates P2P search and browsing.

* studio controls

  A library of controls that can be composed to create instruments, effects
controllers, interfaces to musical programs, and more.  Check out the
[blog](/blog.html) to see a screenshot.

  - [scenegraph](https://scenegraph.dev.java.net/)

* audio waveform visualization

  Take arrays of audio sample data from the synthesizer and display them on a
surface.  Maybe start with simple Java drawing, but eventually we'll want to use
OpenGL for this so we can have fade effects.  This could also get some extra
features like zooming, highlighting regions, and manipulating control points to
create envelope curves.  It would be nice to create a library of filters that
could be applied to an audio buffer or a selection with a right click.  A
stripped down sample viewer and editor I guess.

* synth, instrument and effect database

  A graph database will hold all of the instruments, effects, generators, and
whatever else people want to store, search, browse, and share over the P2P network.

* P2P searching and browsing 

  Browse other peoples collections over the network.  Integrate distributed
search and exploration into the instrument browser widget. 

  - gdbn

* session chat

  A basic text chat panel that lets the members of a session send messages.  It
would be interesting to let code and controls integrate with the chat widget to
do things like automatically send messages related to musical signals.

  -gdbn, [jgroups](http://www.jgroups.org/)?

* session collaboration

  Inspired by NetPD, we want to join into collaborative jamming sessions where
people can live-code, live-patch, and play instruments together.  Each player
will have their own synth server generating audio locally, and commands from
each player will be broadcast to all the other players.  You will see what each
other is manipulating in close to real-time.  We can experiment to see if it
makes sense to quantize control updates to the rhythm or shift updates by a bar.

* networked audio chat

  - [jspeex](http://jspeex.sourceforge.net/)
