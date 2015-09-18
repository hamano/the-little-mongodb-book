PLATEX=uplatex
PANDOC=pandoc
DVIPDFMX=dvipdfmx
DVIPDFMX_OPT=-f otf-up-hiragino

NAME=the-little-mongodb-book-ja
SRC=mongodb.markdown
TEX=$(NAME).tex
PDF=$(NAME).pdf
EPUB=$(NAME).epub
HTML=$(NAME).html
THUMB=$(NAME).png

TEX_TEMPLATE=template.tex
EPUB_TEMPLATE=template.html
EPUB_CSS=test.css

PANDOC_OPT=-f markdown+yaml_metadata_block --toc -N --chapters
PANDOC_TEX_OPT=$(PANDOC_OPT) -t latex --template=$(TEX_TEMPLATE) --listings
PANDOC_EPUB_OPT=$(PANDOC_OPT) -t epub3 --template=$(EPUB_TEMPLATE)

%.dvi: %.tex
	$(PLATEX) $<
	$(PLATEX) $<

%.pdf: %.dvi
	$(DVIPDFMX) $(DVIPDFMX_OPT) $^

%.png: %.pdf
	pdftoppm -png -l 1 $^ > $@

all: $(PDF) $(EPUB) $(THUMB)

clean:
	rm -rf *.log *.out *.aux *.toc $(TEX) $(DVI) $(PDF) $(EPUB) $(HTML) $(THUMB)

$(EPUB): $(SRC) $(EPUB_TEMPLATE)
	$(PANDOC) $(PANDOC_EPUB_OPT) -o $@ $<

$(HTML): $(SRC)
	$(PANDOC) -o $@ $<

$(TEX): $(SRC) $(TEX_TEMPLATE)
	$(PANDOC) $(PANDOC_TEX_OPT) $< > $@

$(DVI): $(TEX)

$(PDF): $(DVI)
