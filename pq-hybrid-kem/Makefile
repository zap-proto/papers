# Build the paper. Requires a TeX distribution with pdflatex + biber/bibtex.
#
# Usage:
#   make            # build main.pdf
#   make clean      # remove auxiliary files
#   make distclean  # also remove main.pdf

LATEX  ?= pdflatex
BIBTEX ?= bibtex
DOC    := main

all: $(DOC).pdf

$(DOC).pdf: $(DOC).tex refs.bib
	$(LATEX) -interaction=nonstopmode $(DOC).tex
	$(BIBTEX) $(DOC) || true
	$(LATEX) -interaction=nonstopmode $(DOC).tex
	$(LATEX) -interaction=nonstopmode $(DOC).tex

clean:
	rm -f $(DOC).aux $(DOC).bbl $(DOC).blg $(DOC).log $(DOC).out \
	      $(DOC).toc $(DOC).bcf $(DOC).run.xml $(DOC).fls $(DOC).fdb_latexmk

distclean: clean
	rm -f $(DOC).pdf

.PHONY: all clean distclean
