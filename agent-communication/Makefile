# Makefile for the ZAP-MCP / ZAP-A2A paper
#
# Targets:
#   make           build main.pdf
#   make clean     remove build artefacts
#   make watch     rebuild on file change (requires latexmk)
#   make check     verify pdflatex/bibtex available

PAPER := main
TEX_FILES := $(PAPER).tex
BIB_FILES := refs.bib
PDF := $(PAPER).pdf

LATEX := pdflatex
LATEX_FLAGS := -interaction=nonstopmode -halt-on-error
BIBTEX := bibtex

.PHONY: all clean watch check distclean

all: $(PDF)

$(PDF): $(TEX_FILES) $(BIB_FILES)
	$(LATEX) $(LATEX_FLAGS) $(PAPER)
	$(BIBTEX) $(PAPER)
	$(LATEX) $(LATEX_FLAGS) $(PAPER)
	$(LATEX) $(LATEX_FLAGS) $(PAPER)

watch:
	latexmk -pdf -pvc -interaction=nonstopmode $(PAPER).tex

check:
	@command -v $(LATEX) >/dev/null 2>&1 || { echo "pdflatex not installed"; exit 1; }
	@command -v $(BIBTEX) >/dev/null 2>&1 || { echo "bibtex not installed"; exit 1; }
	@echo "LaTeX toolchain present."

clean:
	rm -f $(PAPER).aux $(PAPER).log $(PAPER).bbl $(PAPER).blg \
	      $(PAPER).out $(PAPER).toc $(PAPER).fls $(PAPER).fdb_latexmk \
	      $(PAPER).synctex.gz

distclean: clean
	rm -f $(PDF)
