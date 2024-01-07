# This Makefile shall be designed to look for all possible chapters (in all folders except ./build ), include them in main Postavy.tex file and compile main file


# a location where the texmaker packages to be included are located
# (TEXINPUTS is pdflatex's env variable)
TEXINPUTS=$(dir $(abspath $(MAKEFILE_LIST)))../references//:
SSS=~/texmaker-packages//:

# Makefiles that are used to generate separate pdfs for each character
DIRS:=$(filter-out templates/,$(wildcard */))

CHARACTER_PDF="postavy.pdf"
PDF_FILES=$(filter-out templates/*, $(wildcard */build/*.pdf))

# templates to pass via -create command
TEMPLATE_DIR="templates"
TEMPLATE_TEX="character_template.tex"
TEMPLATE_MAKEFILE="Makefile"


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
		make run -C $$dir;	\
	done;					
	@echo All character .pdf files has been created...

.PHONY chars:
chars:
	$(foreach dir, $(DIRS), make run -C $(abspath $(dir))/)
	# TODO make this working and replace 'characters' by it
	# (for loop shall be implemented via Makefile, not bash)
	@echo lol


.PHONY clear:
clear:
	@for dir in $(DIRS);	\
	do						\
		cd $$dir;			\
		make clear;			\
		cd ..;				\
	done
	$(if $(wildcard $(CHARACTER_PDF)), @rm $(CHARACTER_PDF),)
	@echo All .pdf files has been deleted...




# auxiliary macro to create character
define CHAR_CREATE
	@mkdir $(NAME)
	@cp $(TEMPLATE_DIR)/$(TEMPLATE_TEX) $(NAME)/$(NAME).tex
	@cp $(TEMPLATE_DIR)/$(TEMPLATE_MAKEFILE) $(NAME)/$(TEMPLATE_MAKEFILE)
	@echo character $(NAME) has been created...
endef

.PHONY create:
create:
	$(if $(NAME),$(if $(filter $(NAME)/,$(wildcard */)), @echo character with name $(NAME) already exists..., $(CHAR_CREATE) ), @echo variable NAME is not defined. Pass it via 'make create NAME=<name>')


