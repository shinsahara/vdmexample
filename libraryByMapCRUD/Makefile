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
OUTDOC = VPP-Intro

# VDM files
VPPFILES = $(VPPFILES1) $(VPPFILES2) $(RQFILE) $(UTILITYFILES)
		
VPPFILES1 = \
	Test/MyCRUDlib_TestCases.vdmpp BLogic/Library1.vpp \

RQFILE = \
	ReqDict/LibraryRQ1.vdmpp 
	
UTILITYFILES = \
	./Utilities/Character.vpp	./Utilities/Sequence.vpp	./Utilities/String.vpp \
	./CRUDlib/CRUD_map.vdmpp \
	./lib/IO.vdmpp	./lib/VDMUnit.vdmpp	./lib/VDMUtil.vdmpp
	
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

# run VDMJ
vdmj:
	vdmj_UTF8 -r classic -exceptions -e "run()" $(VPPFILES1) $(RQFILE) $(UTILITYFILES)
	echo  "you have to type 'latex' and 'q'"
	vdmj_UTF8 -r classic -exceptions $(VPPFILES1) $(RQFILE) $(UTILITYFILES) 
	echo  "you have to type 'latex' and 'q'"
	$(PLATEX) $(OUTDOC)
	$(BIBTEX) $(OUTDOC)
	makeindex $(OUTDOC).idx
	$(PLATEX) $(OUTDOC)
	$(PLATEX) $(OUTDOC)
	$(DVIPDFM) $(OUTDOC)

vdmjdebug:
	vdmj_UTF8 -exceptions $(VPPFILES2) $(UTILITYFILES)

# Command-Line Interface to Overture
overture:
	overture -vdmpp -i -e "test蔵書を追加する1()" $(VPPFILES)	

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