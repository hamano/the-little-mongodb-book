include meta.mk

PLATEX=uplatex
PANDOC=~/.cabal/bin/pandoc
#PANDOC=pandoc
#PANDOC_OPT=--toc --listings --base-header-level=1 --chapters
PANDOC_OPT=--toc --listings -N
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
	$(PANDOC) -o $@ $<

$(HTML): $(SRC)
	$(PANDOC) -o $@ $<

$(TEX): $(SRC) $(TEMPLATE)
	$(PANDOC) -f markdown -t latex $(PANDOC_OPT) -V version="$(VERSION)" -V pdf_author="$(PDF_AUTHOR)" -V pd_keywords="$(PDF_KEYWORDS)" --template=$(TEMPLATE) $< > $@

$(DVI): $(TEX)

$(PDF): $(DVI)
