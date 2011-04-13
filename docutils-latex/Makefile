#
# Makefile
# Adrian Perez, 2006-05-12 18:49
#

ifdef V
	ifeq ($(origin V),command line)
    VERBOSE := 1
  endif
endif

ifneq ($(VERBOSE),1)
  MAKEFLAGS += s
endif


BASHDOC = bashdoc \
	-cmt-string='%%' \
	-output-dir=doc

RST2TEX = rst2latex.py \
	--documentclass=scrartcl \
	--documentoptions=DIVcalc,11pt \
	--table-style=booktabs \
	--use-latex-footnotes \
	--use-latex-citations \
	--use-latex-docinfo \
	--use-latex-toc

all: doc

doc: doc-txt doc-pdf doc-html

doc/connectical.txt: connectical.cls
	@echo "[1;32m *[0;0m bashdoc  [1;33m$(@)[0;0m"
	$(RM) $@
	$(BASHDOC) text $<

doc/connectical.html doc/default.css: connectical.cls
	@echo "[1;32m *[0;0m bashdoc  [1;33m$(@)[0;0m"
	$(RM) $@
	$(BASHDOC) html $<

%.tex: %.txt
	@echo "[1;32m *[0;0m docutils [1;33m$(@)[0;0m"
	$(RM) $@
	$(RST2TEX) $< $@

%.pdf %.log %.log %.lot %.aux %.toc %.out: %.tex
	@echo "[1;32m *[0;0m pdflatex [1;33m$(@)[0;0m"
	mkdir -p $(dir $@)
	( cd $(dir $@) ; \
		pdflatex --interaction=batchmode $(notdir $<) && \
		pdflatex --interaction=batchmode $(notdir $<) ) \
	> /dev/null


doc-txt:  doc/connectical.txt
doc-pdf:  doc/connectical.pdf
doc-html: doc/connectical.html doc/default.css


clean:
	@echo "[1;32m *[0;0m clean"
	$(RM) doc/*


# Mark LaTeX side-effect stuff as intermediate files.
.INTERMEDIATE: doc/connectical.log doc/connectical.lof \
	doc/connectical.lot doc/connectical.toc doc/connectical.aux \
	doc/connectical.out

.PHONY: install doc doc-html doc-pdf doc-txt

# vim:ft=make
#

