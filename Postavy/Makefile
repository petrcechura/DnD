# This Makefile shall be designed to look for all possible chapters (in all folders except ./build ), include them in main Postavy.tex file and compile main file


# a location where the texmaker packages to be included are located
# (TEXINPUTS is pdflatex's env variable)
# TODO make this relative to project's path (in references)
TEXINPUTS=$(shell pwd)/../references//:
SSS=~/texmaker-packages//:

# Makefiles that are used to generate separate pdfs for each character
DIRS=$(shell find -maxdepth 1 -mindepth 1 -type d)

CHARACTER_PDF="postavy.pdf"
PDF_FILES=$(shell find -mindepth 2 -name "*.pdf")

# templates to pass via -create command
TEMPLATE_DIR="templates"
TEMPLATE_TEX="character_template.tex"
TEMPLATE_MAKEFILE="Makefile"

# name of a new character created via -create command
NAME?=""

.PHONY help:
help:
	@echo 'help'    	        -- displays this message
	@echo 'compile' 	        -- creates main pdf including all the characters
	@echo 'characters'	        -- creates just separate character pdfs in their dirs
	@echo 'create NAME=<name>'   -- create a new character folder and template
	@echo Directories to be processed: $(DIRS)


.PHONY compile:
compile: characters
	@export TEXINPUTS 
	@pdfunite $(PDF_FILES) $(CHARACTER_PDF)
	@echo Master $(CHARACTER_PDF) file has been compiled...

.PHONY characters:
characters:
	@for dir in $(DIRS); 	\
	do 						\
		cd $$dir;  			\
		make run;			\
		cd ..;				\
	done;					
	@echo All character .pdf files has been created...

.PHONY clear:
clear:
	@for dir in $(DIRS);	\
	do						\
		cd $$dir;			\
		make clear;			\
		cd ..;				\
	done
	@rm postavy.pdf
	@echo All .pdf files has been deleted...

.PHONY create:
create:
	@if [ -z $(NAME) ];		\
	then					\
		echo missing NAME variable, pass it via 'make create NAME=<name>';	\
		exit 1;				\
	elif [ -e $(NAME) ];	\
	then				\
		echo that character already exists...;	\
		exit 2;			\
	fi
	@mkdir $(NAME)
	@cp $(TEMPLATE_DIR)/$(TEMPLATE_TEX) $(NAME)/$(NAME).tex
	@cp $(TEMPLATE_DIR)/$(TEMPLATE_MAKEFILE) $(NAME)/$(TEMPLATE_MAKEFILE)
	@echo character $(NAME) has been created...

