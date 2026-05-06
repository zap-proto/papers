PAPER = main
PROOF = ../../proofs/transport-vs-jwt/proof

LATEXMK ?= latexmk
PDFLATEX ?= pdflatex
BIBER ?= biber

LATEXMK_FLAGS = -pdf -interaction=nonstopmode -halt-on-error -file-line-error

.PHONY: all paper proof clean distclean check

all: paper proof

paper: $(PAPER).pdf

proof:
	$(MAKE) -C ../../proofs/transport-vs-jwt

$(PAPER).pdf: $(PAPER).tex refs.bib
	@if command -v $(LATEXMK) >/dev/null 2>&1; then \
		$(LATEXMK) $(LATEXMK_FLAGS) $(PAPER).tex; \
	else \
		$(PDFLATEX) -interaction=nonstopmode $(PAPER).tex; \
		$(BIBER) $(PAPER); \
		$(PDFLATEX) -interaction=nonstopmode $(PAPER).tex; \
		$(PDFLATEX) -interaction=nonstopmode $(PAPER).tex; \
	fi

# Syntax-only check; does not require a TeX engine.
# Verifies braces balance and no obvious LaTeX disasters.
check:
	@awk 'BEGIN{o=0;c=0} {for(i=1;i<=length($$0);i++){ch=substr($$0,i,1); if(ch=="{")o++; else if(ch=="}")c++}} END{print "open:",o,"close:",c; if(o!=c){exit 1}}' $(PAPER).tex
	@grep -n '\\begin{' $(PAPER).tex | wc -l | xargs -I{} echo "begin envs: {}"
	@grep -n '\\end{'   $(PAPER).tex | wc -l | xargs -I{} echo "end   envs: {}"

clean:
	rm -f *.aux *.bbl *.bcf *.blg *.fdb_latexmk *.fls *.log *.out *.run.xml *.toc *.synctex.gz

distclean: clean
	rm -f $(PAPER).pdf
