# the .tex file shall have the same name as the directory
NAME=$(shell find -name *.tex)

CWD=$(dir $(abspath $(MAKEFILE_LIST)))

.PHONY help:
help:
	@echo to be defined...


.PHONY run:
run:
	$(if $(wildcard $(CWD)/build),, @mkdir ./build)
	@pdflatex -output-directory $(CWD)/build $(NAME)

.PHONY clear:
clear:
	$(if $(wildcard $(CWD)/build/), @rm -rf build, @echo nothing...)
