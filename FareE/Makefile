###########################
# Auto VDM -> TeX report
###########################

## Definitions
#################

#encode
CODE=UTF8
# TeX commands
TEXDIR = /usr/local/texlive/2018/bin/x86_64-darwin
#TEXDIR = /usr/bin  # Ubuntu 10.10
# PLATEX = platex
#PLATEX = dotexshop
PLATEX = $(TEXDIR)/platex
#BIBTEX=jbibtex
BIBTEX=pbibtex --kanji=$(CODE)
#DVIPDFM = dvipdfmx
DVIPDFM = $(TEXDIR)/dvipdfmx
EBB = ebb

# VDMTools command line
VPPDE = vppde

# Output document name
OUTDOC = Fare

# VPP files
VPPFILES = \
CalcFare.vdmpp			route_search.vdmpp \
FareTableDic.vdmpp		dijkstra.vdmpp			route_search_by_dijkstra.vdmpp \
MyTest.vdmpp			MyTestCase.vdmpp	route_search_testspec.vdmpp \
UseFare.vdmpp			railway_network_data.vdmpp \
VDMUnit.vpp			railway_network.vdmpp \
lib/IO.vdmpp	lib/MATH.vdmpp	lib/VDMUtil.vdmpp

# Test script name
TESTSCRIPT1 = test1.script
TESTSCRIPT2 = test2.script
# Image directory
IMGDIR = image

## Make
#################

# make target
all: $(OUTDOC)

$(OUTDOC):  makevdmtex
	ebb image/*.jpg
	$(PLATEX) $(OUTDOC)
	$(BIBTEX) $(OUTDOC)
#	makeindex  $(OUTDOC).idx
	$(PLATEX) $(OUTDOC)
	$(PLATEX) $(OUTDOC)
	$(DVIPDFM) $(OUTDOC)

# run VDMTools
makevdmtex:
	# Read & Syntax check
	LANG=ja_JP.$(CODE) $(VPPDE) -p $(VPPFILES)
	# Type check
	LANG=ja_JP.$(CODE) $(VPPDE) -t $(VPPFILES)
	# Run Interpreter with TESTSCRIPT
	LANG=ja_JP.$(CODE) $(VPPDE) -y -i -D -I -P -Q -R vdm1.tc $(TESTSCRIPT1) $(VPPFILES)
	# Run Interpreter with "set exception" option
	LANG=ja_JP.$(CODE) time $(VPPDE) -y -i -D -I -P -Q -R vdm2.tc $(TESTSCRIPT2) $(VPPFILES)
	# Pretty print
	LANG=ja_JP.$(CODE) $(VPPDE)  -l -r $(VPPFILES) 
	#marge Test Coverage files
	mergetc vdm1.tc vdm2.tc > vdm.tc

# Clean files. But Output document is not deleted.
clean:
	rm -rf *.aux *.log *.bbl *.blg *.dvi *.toc *.ilg *.ind
	rm -rf *.out *.v*pp.tex *.v*pp.tex *.idx vdm.tc *.java
	rm -rf image/*.bb vdm*.tc

# Clean output document
realclean: clean
	rm -rf $(OUTDOC).pdf
