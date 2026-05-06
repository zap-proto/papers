PAPER = main
LATEX = pdflatex
BIBTEX = bibtex
LATEX_FLAGS = -interaction=nonstopmode -halt-on-error

.PHONY: all clean check

all: $(PAPER).pdf

$(PAPER).pdf: $(PAPER).tex refs.bib
	$(LATEX) $(LATEX_FLAGS) $(PAPER).tex
	$(BIBTEX) $(PAPER) || true
	$(LATEX) $(LATEX_FLAGS) $(PAPER).tex
	$(LATEX) $(LATEX_FLAGS) $(PAPER).tex

check:
	@command -v $(LATEX) >/dev/null 2>&1 || { echo "pdflatex not installed"; exit 1; }
	@$(LATEX) $(LATEX_FLAGS) -draftmode $(PAPER).tex >/dev/null && echo "OK: $(PAPER).tex compiles"

clean:
	rm -f $(PAPER).aux $(PAPER).log $(PAPER).out $(PAPER).bbl $(PAPER).blg \
	      $(PAPER).toc $(PAPER).pdf $(PAPER).fdb_latexmk $(PAPER).fls
