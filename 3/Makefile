GNUPLOT  := gnuplot
PDFLATEX := pdflatex
OUTDIR   := output

FIGS := $(basename $(wildcard *.gpt))

.PHONY: all
all: $(FIGS)

.PHONY: $(FIGS)
$(FIGS): %: %.pdf

# -------- Pipeline --------
%.pdf: %.gpt | $(OUTDIR)
	@echo "==> Running gnuplot for $*"
	$(GNUPLOT) $*.gpt
	@echo "==> Running pdflatex for $*"
	$(PDFLATEX) -interaction=nonstopmode $*.tex
	@echo "==> Removing intermediate PDFs"
	@rm -f *-inc.pdf
	@echo "==> Moving final PDF to $(OUTDIR)/"
	@mv -f $*.pdf $(OUTDIR)/

$(OUTDIR):
	@mkdir -p $(OUTDIR)

.PHONY: clean
clean:
	@rm -f *.aux *.log *.out *.toc *.pdf *-inc.pdf *.tex
	@rm -rf $(OUTDIR)

.PHONY: distclean
distclean: clean
	@rm -rf $(OUTDIR)
