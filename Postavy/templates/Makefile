# the .tex file shall have the same name as the directory
NAME=$(shell find -name *.tex)

.PHONY help:
help:
	@echo to be defined...


.PHONY run:
run:
	@if [ -z $(shell ls | grep build) ]; then mkdir ./build; fi
	@pdflatex -output-directory build $(NAME)

.PHONY clear:
clear:
	@rm -rf build
