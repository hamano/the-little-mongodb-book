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
SRC=$(NAME).markdown
TEX=$(NAME).tex
PDF=$(NAME).pdf
EPUB=$(NAME).epub
HTML=$(NAME).html

TEX_TEMPLATE=template.tex
EPUB_TEMPLATE=template.epub3

%.dvi: %.tex
	$(PLATEX) $<
	$(PLATEX) $<

%.pdf: %.dvi
	$(DVIPDFMX) $(DVIPDFMX_OPT) $^

all: $(PDF) $(EPUB)

clean:
	rm -rf *.log *.out *.aux *.toc $(TEX) $(DVI) $(PDF) $(EPUB) $(HTML)

$(EPUB): $(SRC) $(EPUB_TEMPLATE)
	$(PANDOC) $(PANDOC_OPT) -t epub3 --template=$(EPUB_TEMPLATE) -o $@ $<

$(HTML): $(SRC)
	$(PANDOC) -o $@ $<

$(TEX): $(SRC) $(TEX_TEMPLATE)
	$(PANDOC) $(PANDOC_OPT) -t latex --template=$(TEX_TEMPLATE) $< > $@

$(DVI): $(TEX)

$(PDF): $(DVI)
