# To build, install:
#   - Ruby
#   - Gems: asciidoctor, asciidoctor-diagram, and coderay
# then run `make`

book: index.html

index.html: sources/*.adoc
	bundle exec asciidoctor -o index.html -b html5 -r asciidoctor-diagram sources/main.adoc

