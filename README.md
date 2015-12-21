# codemining

Experimental implementation of "code mining", as defined in the
[World Wide Hack Manifesto](https://github.com/WorldWideHack/manifesto).

For a description of the implementation approach, see [doc/implementation_ideas.md](doc/implementation_ideas.md).

## OCaml as primary implementation language

I am using OCaml as the primary implementation language for code mining because, although I lament its weak momentum, I love it. The OCaml community seems to have recently gained strength -- in particular, Cambridge's [OCaml Labs](http://www.cl.cam.ac.uk/projects/ocamllabs/) has provided some leadership and manpower that encourages me greatly.

Whether OCaml itself gains momentum or not, I see it as a model for future statically typed functional programming languages (including and beyond F#) that could become widely accepted.
  
## JavaScript as first target

JavaScript is the first target for code mining, for the following reasons:

* It is an extremely popular language.

* An excellent JavaScript source analyzer, [Facebook Flow](http://flowtype.org), is written in OCaml.

* A deep understanding of JavaScript will be valuable to me (Dean Thompson) personally, in my role
  as CTO of [Nowait](http://nowait.com).
