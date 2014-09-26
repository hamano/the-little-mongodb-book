#include meta.mk

PLATEX=uplatex
PANDOC=~/.cabal/bin/pandoc
#PANDOC=pandoc
PANDOC_OPT=-f markdown+yaml_metadata_block --toc --listings -N --chapters
PANDOC_EPUB_OPT=
DVIPDFMX=dvipdfmx
DVIPDFMX_OPT=-f uptex-hiragino
#DVIPDFMX_OPT=-f uptex-hiramaru.map

NAME=mongodb
TEMPLATE=$(NAME).tmpl
SRC=$(NAME).markdown
TEX=$(NAME).tex
PDF=$(NAME).pdf
EPUB=$(NAME).epub
HTML=$(NAME).html

%.dvi: %.tex
	$(PLATEX) $<
	$(PLATEX) $<

%.pdf: %.dvi
	$(DVIPDFMX) $(DVIPDFMX_OPT) $^

all: $(PDF) $(EPUB)

clean:
	rm -rf *.log *.out *.aux *.toc $(TEX) $(DVI) $(PDF) $(EPUB) $(HTML)

$(EPUB): $(SRC)
	$(PANDOC) $(PANDOC_EPUB_OPT) -o $@ $<

$(HTML): $(SRC)
	$(PANDOC) -o $@ $<

$(TEX): $(SRC) $(TEMPLATE)
	$(PANDOC) $(PANDOC_OPT) -t latex --template=$(TEMPLATE) $< > $@

$(DVI): $(TEX)

$(PDF): $(DVI)
