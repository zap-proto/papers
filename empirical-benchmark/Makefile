# results.tex is generated from the harness output; main.tex holds no measured
# literal, so the paper cannot print a figure the output does not contain. If
# the output is beside this checkout, `all' regenerates before building and the
# fragment cannot be stale. If it is not, the build uses the committed
# fragment, whose header names the run it came from.
BENCH := ../../bench/bench-results.txt

.PHONY: all clean results verify
all: results main.pdf

results:
	@if [ -f $(BENCH) ]; then ./emit.py $(BENCH) || \
	   echo "keeping the committed results.tex"; \
	 else echo "no $(BENCH); building from the committed results.tex"; fi

main.pdf: main.tex results.tex
	latexmk -pdf -halt-on-error -Werror main.tex

# Does the committed fragment still describe the harness output on disk?
verify:
	@test -f $(BENCH) || { echo "no $(BENCH) to verify against"; exit 0; }
	@./emit.py $(BENCH) >/dev/null && git diff --quiet -- results.tex \
	  && echo "results.tex matches $(BENCH)" \
	  || { echo "results.tex is stale: run make and commit the fragment"; \
	       git --no-pager diff --stat -- results.tex; exit 1; }

clean:
	latexmk -C main.tex
