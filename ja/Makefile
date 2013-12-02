include meta.mk

PLATEX=platex
PANDOC=pandoc
PANDOC_OPT=--toc --listings

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
	dvipdfmx $^

all: $(PDF) $(EPUB)

clean:
	rm -rf *.log *.out *.aux *.toc $(TEX) $(DVI) $(PDF) $(EPUB) $(HTML)

$(EPUB): $(SRC)
	$(PANDOC) -o $@ $<

$(HTML): $(SRC)
	$(PANDOC) -o $@ $<

$(TEX): $(SRC) $(TEMPLATE)
	$(PANDOC) -f markdown -t latex --base-header-level=1 --chapters $(PANDOC_OPT) -V version="$(VERSION)" -V keywords="$(KEYWORDS)" --template=$(TEMPLATE) $< > $@

$(DVI): $(TEX)

$(PDF): $(DVI)
