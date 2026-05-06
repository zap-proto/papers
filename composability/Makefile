PAPER=main
LATEX=pdflatex
BIBER=biber
LATEXFLAGS=-interaction=nonstopmode -halt-on-error

.PHONY: all clean view

all: $(PAPER).pdf

$(PAPER).pdf: $(PAPER).tex refs.bib
	$(LATEX) $(LATEXFLAGS) $(PAPER).tex
	$(BIBER) $(PAPER) || true
	$(LATEX) $(LATEXFLAGS) $(PAPER).tex
	$(LATEX) $(LATEXFLAGS) $(PAPER).tex

clean:
	rm -f *.aux *.bbl *.bcf *.blg *.log *.out *.run.xml *.toc *.synctex.gz $(PAPER).pdf

view: $(PAPER).pdf
	open $(PAPER).pdf
