THISDIR := phy450-relativisticEandM
THISBOOK := phy450
THISBOOK_DEPS += poppitz.tex

include make.revision
include ../latex/make.bookvars

# Override my default:
MY_CLASSICTHESIS_FRONTBACK_FILES := $(filter-out ../classicthesis_mine/FrontBackmatter/Contents.tex,$(MY_CLASSICTHESIS_FRONTBACK_FILES))
MY_CLASSICTHESIS_FRONTBACK_FILES := $(filter-out ../classicthesis_mine/FrontBackmatter/Version.tex,$(MY_CLASSICTHESIS_FRONTBACK_FILES))
MY_CLASSICTHESIS_FRONTBACK_FILES := $(filter-out ../classicthesis_mine/FrontBackmatter/Bibliography.tex,$(MY_CLASSICTHESIS_FRONTBACK_FILES))

#ONCEFLAGS := -justonce

#SOURCE_DIRS += appendix
SOURCE_DIRS += solutions
SOURCE_DIRS += lectures
SOURCE_DIRS += problems

FIGURES := ../figures/$(THISDIR)
SOURCE_DIRS += $(FIGURES)

#GENERATED_SOURCES += matlab.tex
#GENERATED_SOURCES += julia.tex
GENERATED_SOURCES += mathematica.tex
GENERATED_SOURCES += poppitz.tex

EPS_FILES := $(wildcard $(FIGURES)/*.eps)
PDFS_FROM_EPS := $(subst eps,pdf,$(EPS_FILES))

THISBOOK_DEPS += $(PDFS_FROM_EPS)
#THISBOOK_DEPS += macros_mathematica.sty

#CLEAN_TARGETS += ps5mathematica.tex ps9mathematica.tex
CLEAN_TARGETS += *.sp
#CLEAN_TARGETS += FrontBackmatter/*.sp

#SPELLCHECK := $(patsubst %.tex,%.sp,$(wildcard *.tex))
#DO_SPELL_CHECK := $(shell cat spellcheckem.txt)
#SPELLCHECK := $(patsubst %.tex,%.sp,$(DO_SPELL_CHECK))

include ../latex/make.rules

#$(THISBOOK).pdf :: $(shell cat spellcheckem.txt)

#.PHONY: spellcheck
#spellcheck: $(SPELLCHECK)

%.sp : %.tex
	spellcheck $^
	touch $@

mmacells/mmacells.sty:
	git clone https://github.com/jkuczm/mmacells

bib:
	rm -f Bibliography.bib myrefs.bib
	make Bibliography.bib myrefs.bib

mmacells.sty: mmacells/mmacells.sty
	cp $^ $@

#julia.tex : ../julia/METADATA
#mathematica.tex : ../mathematica/METADATA
#matlab.tex : ../matlab/METADATA

%.sp : %.tex
	spellcheck $^
	touch $@

backmatter.tex : ../latex/classicthesis_mine/backmatter.tex
	cp $< $@

poppitz.tex : mkpref
	./mkpref > $@

clean ::
	git checkout FrontBackmatter/Contents.tex
	git checkout FrontBackmatter/Version.tex
	git checkout FrontBackmatter/Bibliography.tex
	git checkout $(THISBOOK).tex
