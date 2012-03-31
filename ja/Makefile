all: mongodb.dvi

mongodb.tex: mongodb.markdown
	pandoc -f markdown -t latex --base-header-level=1 --chapters --template=book.tmpl $^ | nkf -j > $@

mongodb.dvi: mongodb.tex
	platex $^

mongodb.pdf: mongodb.dvi
	dvipdfm $^
