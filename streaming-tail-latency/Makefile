PAPER = main
TEX   = pdflatex -interaction=nonstopmode -halt-on-error
BIB   = bibtex

all: $(PAPER).pdf

$(PAPER).pdf: $(PAPER).tex refs.bib
	$(TEX) $(PAPER).tex
	-$(BIB) $(PAPER) || true
	$(TEX) $(PAPER).tex
	$(TEX) $(PAPER).tex

check:
	$(TEX) -draftmode $(PAPER).tex

clean:
	rm -f $(PAPER).aux $(PAPER).log $(PAPER).out $(PAPER).toc \
	      $(PAPER).bbl $(PAPER).blg $(PAPER).pdf

.PHONY: all check clean
