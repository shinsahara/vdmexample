###########################
# Auto VDM -> TeX report
###########################

## Definitions
#################

HOME = /Users/sahara
VPPHOME = $(HOME)/vdmpp
VPPDE = $(VPPHOME)/bin/vppde

#encode
#CODE = SJIS
CODE = UTF8

# TeX commands
TEXDIR = /usr/local/texlive/2016/bin/x86_64-darwin
PLATEX = $(TEXDIR)/platex --kanji=$(CODE)
#BIBTEX=jbibtex
BIBTEX=pbibtex --kanji=$(CODE)
DVIPDFM = $(TEXDIR)/dvipdfmx
EBB = extractbb

# VDMTools command line
VPPDE = vppde

#VDMJ
VDMJ = vdmj_UTF8

# Output document name
OUTDOC = ATC

# VDM files
DEFAULTFILES = MyTest.vdmpp 
VPPFILES =  \
	MyTestCase.vdmpp \
	ATC.vdmpp ATC_Terminology.vdmpp \
	PrintTestListener.vdmpp 

LIBFILES = \
	./lib/VDMUnit.vdmpp ./lib/IO.vdmpp ./lib/VDMUtil.vdmpp
	
# Test script name
TESTSCRIPT = test.script

# Image directory
IMGDIR = image

## Make
#################

# make target
all: $(OUTDOC)

$(OUTDOC):  makevdmtex
#$(OUTDOC): 
	$(PLATEX) $(OUTDOC)
	$(BIBTEX) $(OUTDOC)
	makeindex $(OUTDOC).idx
	$(PLATEX) $(OUTDOC)
	$(PLATEX) $(OUTDOC)
	$(DVIPDFM) $(OUTDOC)

# run VDMTools
makevdmtex:
	# Read & Syntax check
	LANG=ja_JP.$(CODE) $(VPPDE) -p $(DEFAULTFILES) $(VPPFILES) $(LIBFILES) 
	# Type check
	LANG=ja_JP.$(CODE) $(VPPDE) -t $(DEFAULTFILES) $(VPPFILES) $(LIBFILES) 
	# Run Interpreter with TESTSCRIPT
	LANG=ja_JP.$(CODE) $(VPPDE) -y -i -D -I -P -Q -R vdm.tc $(TESTSCRIPT) $(DEFAULTFILES) $(VPPFILES) $(LIBFILES) 
	# Pretty print
	LANG=ja_JP.$(CODE) $(VPPDE)  -l -r $(DEFAULTFILES) $(VPPFILES)$(LIBFILES) 

# Command-Line Interface to Overture
overture:
	overture -vdmpp -i -e "run()" $(DEFAULTFILES) $(VPPFILES) $(LIBFILES) 

# Clean files. But Output document is not deleted.
clean:
	rm -rf *.aux *.aux *.log *.bbl *.blg *.dvi *.toc *.ilg *.ind *.bak
	rm -rf */*.aux */*.log */*.bbl */*.blg */*.dvi */*.toc */*.ilg */*.ind */*.bak
	rm -rf *.out *.vpp.tex *.vdmpp.tex *.idx */vdm.tc
	rm -rf */*.out */*.vpp.tex */*.vdmpp.tex */*.idx */vdm.tc
	rm -rf image/*.bb

# Clean output document
realclean: clean
	rm -rf $(OUTDOC).pdf