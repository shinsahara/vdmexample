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
OUTDOC = Library

# VDM files
VPPFILES = $(VPPFILES1) $(RQFILE) $(UTILITYFILES)
		
VPPFILES1 = \
	Test/MyCRUDlib_TestCases.vdmpp BLogic/Library1.vpp \

RQFILE = \
	ReqDict/LibraryRQ1.vdmpp 
	
UTILITYFILES = \
	./lib/VDMUnit.vdmpp	./lib/IO.vdmpp	./lib/VDMUtil.vdmpp ./CRUDlib/CRUD_map.vdmpp
	
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
	LANG=ja_JP.$(CODE) $(VPPDE) -p $(VPPFILES1) $(RQFILE) $(UTILITYFILES)
	# Type check
	LANG=ja_JP.$(CODE) $(VPPDE) -t $(VPPFILES1) $(RQFILE) $(UTILITYFILES)
	# Run Interpreter with TESTSCRIPT
	LANG=ja_JP.$(CODE) $(VPPDE) -y -i -D -I -P -Q -R vdm1.tc $(TESTSCRIPT) $(VPPFILES1) $(RQFILE) $(UTILITYFILES)
	# Pretty print
	LANG=ja_JP.$(CODE) $(VPPDE)  -l -r $(VPPFILES)

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