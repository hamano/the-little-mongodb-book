all: mongodb.dvi

clean:
	rm -rf *.tex *.log *.out *.aux *.dvi *.pdf *.epub

mongodb.epub: mongodb.markdown
	pandoc -o $@ $^

mongodb.tex: mongodb.markdown
	pandoc -f markdown -t latex --base-header-level=1 --chapters --template=mongodb.tmpl $^ | nkf -j > $@

mongodb.dvi: mongodb.tex
	platex $^

mongodb.pdf: mongodb.dvi
	dvipdfm $^
