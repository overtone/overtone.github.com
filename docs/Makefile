# To build, install:
#   - Ruby
#   - Gems: asciidoctor, asciidoctor-diagram, and coderay
# then run `make`

book: docs.html

docs.html: sources/*.adoc
	bundle exec asciidoctor -o ../docs.html -b html5 -a stem -r asciidoctor-diagram sources/main.adoc

