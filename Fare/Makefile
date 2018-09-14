###########################
# Auto VDM -> TeX report
###########################

## Definitions
#################

#encode
CODE=UTF8
# TeX commands
TEXDIR = /usr/local/texlive/2018/bin/x86_64-darwin
PLATEX = $(TEXDIR)/platex
#BIBTEX=jbibtex
BIBTEX=pbibtex --kanji=$(C0DE)
DVIPDFM = $(TEXDIR)/dvipdfmx
EBB = ebb

# VDMTools command line
VPPDE = vppde

# Output document name
OUTDOC = Fare

# VPP files
VPPFILES = \
	CalcFare.vdmpp			VDMUnit.vpp			route_search.vdmpp \
	FareTableDic.vdmpp		dijkstra.vdmpp			route_search_by_dijkstra.vdmpp \
	MyTest.vdmpp			io.vpp				route_search_testspec.vdmpp \
	MyTestCase.vdmpp		railway_network_data.vdmpp \
	UseFare.vdmpp			railway_network.vdmpp \

# Test script name
TESTSCRIPT = test.script
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
	makeindex  $(OUTDOC).idx
	$(PLATEX) $(OUTDOC)
	$(PLATEX) $(OUTDOC)
	$(DVIPDFM) $(OUTDOC)

# run VDMTools
makevdmtex:
	# Read & Syntax check
	LANG=ja_JP.$(CODE) $(VPPDE) -p -R vdm.tc $(VPPFILES)
	# Type check
	LANG=ja_JP.$(CODE) $(VPPDE) -t $(VPPFILES)
	# Run Interpreter with TESTSCRIPT
	LANG=ja_JP.$(CODE) $(VPPDE) -y -i -D -I -P -Q -R vdm.tc $(TESTSCRIPT) $(VPPFILES)
	# Pretty print
	LANG=ja_JP.$(CODE) $(VPPDE)  -l -r $(VPPFILES) 
	echo Finish runnning VDMTools

# Clean files. But Output document is not deleted.
clean:
	rm -rf *.aux *.log *.bbl *.blg *.dvi *.toc *.ilg *.ind
	rm -rf *.out *.vpp.tex *.vdmpp.tex *.idx vdm.tc
	rm -rf image/*.bb

# Clean output document
realclean: clean
	rm -rf $(OUTDOC).pdf
