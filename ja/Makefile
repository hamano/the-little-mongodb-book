all: mongodb.pdf mongodb.epub

clean:
	rm -rf *.tex *.log *.out *.aux *.toc *.dvi *.pdf *.epub

mongodb.epub: mongodb.markdown
	pandoc -o $@ $<

mongodb.html: mongodb.markdown
	pandoc -o $@ $<

mongodb.tex: mongodb.tmpl mongodb.markdown
	pandoc -f markdown -t latex --base-header-level=1 --chapters --toc --template=mongodb.tmpl mongodb.markdown > $@

mongodb.dvi: mongodb.tex
	platex $<
	platex $<

mongodb.pdf: mongodb.dvi
	dvipdfmx $^
#	pdftk mongodb.pdf update_info info.txt output the-little-mongodb-book-ja.pdf
