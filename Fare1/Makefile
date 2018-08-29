###########################
# Auto VDM -> TeX report
###########################

## Definitions
#################

#encode
CODE = UTF8
# TeX commands
TEXDIR = /usr/local/texlive/2018/bin/x86_64-darwin
PLATEX = $(TEXDIR)/platex
BIBTEX=pbibtex --kanji=$(C0DE)
DVIPDFM = $(TEXDIR)/dvipdfmx
EBB = ebb

# VDMTools command line
VPPDE = vppde

# Output document name
OUTDOC = Fare1

# VPP files
VPPFILES = \
	Fare1.vdmpp	  Fare1_testspec.vdmpp UseFare1.vdmpp

# Test script name
TESTSCRIPT = test.script
# Image directory
IMGDIR = image

## Make
#################

# make target
all: $(OUTDOC)

$(OUTDOC):  makevdmtex
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

# Clean files. But Output document is not deleted.
clean:
	rm -rf *.aux *.log *.bbl *.blg *.dvi *.toc *.ilg *.ind *.idv *.lg
	rm -rf *.out *.vpp.tex *.vdmpp.tex *.idx vdm.tc
	rm -rf image/*.bb

# Clean output document
realclean: clean
	rm -rf $(OUTDOC).pdf