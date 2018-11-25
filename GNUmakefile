THISDIR := phy450-relativisticEandM
THISBOOK := phy450
THISBOOK_DEPS += poppitz.tex

export BOOKSUBVER := 1
export BOOKMAJVER := 0
# This isn't a good way to version.  It depends on the local git reflog history count.
export REVCOUNTSTART := 1

#.revinfo/gitCommitDateAsMyTime.tex:\newcommand{\myTime}{April 2018}\newcommand{\myVersion}{version V0.117\xspace}
VER := $(shell grep Version .revinfo/gitCommitDateAsMyTime.tex | sed 's/.*{//;s/.xspace.*//;')

include ../latex/make.bookvars

#ONCEFLAGS := -justonce

#SOURCE_DIRS += appendix
SOURCE_DIRS += solutions
SOURCE_DIRS += lectures
SOURCE_DIRS += problems

FIGURES := ../figures/$(THISDIR)
SOURCE_DIRS += $(FIGURES)

# also toggle redacted classicthesis-config.tex
# FIXME: changing this flag should be a dependency of matlab.tex
#REDACTED := -redacted

#GENERATED_SOURCES += matlab.tex
#GENERATED_SOURCES += julia.tex
GENERATED_SOURCES += mathematica.tex
GENERATED_SOURCES += poppitz.tex

SOURCES += noetherCurrentScalarField.tex
SOURCES += scalarFieldCreationOpCommutator.tex
SOURCES += scalarFieldHamiltonian.tex
SOURCES += qftProblemSet1.tex
#SOURCES += qftProblemSet2.tex

EPS_FILES := $(wildcard $(FIGURES)/*.eps)
PDFS_FROM_EPS := $(subst eps,pdf,$(EPS_FILES))

THISBOOK_DEPS += $(PDFS_FROM_EPS)
#THISBOOK_DEPS += macros_mathematica.sty

#CLEAN_TARGETS += ps5mathematica.tex ps9mathematica.tex
CLEAN_TARGETS += *.sp
#CLEAN_TARGETS += FrontBackmatter/*.sp

#SPELLCHECK := $(patsubst %.tex,%.sp,$(wildcard *.tex))
DO_SPELL_CHECK := $(shell cat spellcheckem.txt)
SPELLCHECK := $(patsubst %.tex,%.sp,$(DO_SPELL_CHECK))

include ../latex/make.rules

$(THISBOOK).pdf :: $(shell cat spellcheckem.txt)

.PHONY: spellcheck
spellcheck: $(SPELLCHECK)

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

dropbox:
	cp $(THISBOOK).pdf ~/Dropbox/$(THISDIR)/$(THISBOOK).$(VER).pdf
	git log --decorate > ~/Dropbox/$(THISDIR)/Changelog.txt

dist:
	cp $(THISBOOK).pdf $(THISBOOK).$(VER).pdf

# a for annotate (releases).
tag:
	git tag -a $(THISBOOK).$(VER).pdf

%.sp : %.tex
	spellcheck $^
	touch $@

.PHONY: copy
copy : $(HOME)/Dropbox/$(THISDIR)/$(THISBOOK).pdf

$(HOME)/Dropbox/$(THISDIR)/$(THISBOOK).pdf : $(THISBOOK).pdf
	cp $^ $@

backmatter.tex : ../latex/classicthesis_mine/backmatter.tex
	cp $< $@

poppitz.tex : mkpref
	./mkpref > $@
