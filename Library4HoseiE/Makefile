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
TEXDIR = /usr/local/texlive/2018/bin/x86_64-darwin
PLATEX = $(TEXDIR)/platex
#BIBTEX=jbibtex
BIBTEX=pbibtex --kanji=$(C0DE)
DVIPDFM = $(TEXDIR)/dvipdfmx
EBB = ebb

# VDMTools command line
VPPDE = vppde

#VDMJ
VDMJ = vdmj_UTF8

# Output document name
OUTDOC = Library

# VDM files
VPPFILES = \
	TestApp.vdmpp	UseLibrary.vdmpp	Library.vdmpp		io.vpp

# Test script name
TESTSCRIPT = test.script
# Image directory
IMGDIR = image

## Make
#################
 
# make target
all: $(OUTDOC)

$(OUTDOC):  makevdmtex
	echo makeing PDF document
	$(PLATEX) $(OUTDOC)
#	$(BIBTEX) $(OUTDOC)
#	makeindex  $(OUTDOC).idx
#	$(PLATEX) $(OUTDOC)
	$(PLATEX) $(OUTDOC)
	$(DVIPDFM) $(OUTDOC)

# run VDMTools
makevdmtex:
	# Read & Syntax check
	#LANG=ja_JP.$(CODE) $(VPPDE) -p -R vdm.tc $(VPPFILES)
	# Type check
	LANG=ja_JP.$(CODE) $(VPPDE) -t $(VPPFILES)
	#$(VPPDE) -t $(VPPFILES)
	# Run Interpreter with TESTSCRIPT
	#LANG=ja_JP.$(CODE) $(VPPDE) -i -D -I -P -Q -R vdm.tc $(TESTSCRIPT) $(VPPFILES)
	#$(VPPDE) -i -D -I -P -Q -R vdm.tc $(TESTSCRIPT) $(VPPFILES)
	# Run Interpreter with "set exception" option
	LANG=ja_JP.$(CODE) time $(VPPDE) -y -i -D -I -P -Q -R vdm.tc $(TESTSCRIPT) $(VPPFILES)
	# Pretty print
	LANG=ja_JP.$(CODE) $(VPPDE)  -l -r $(VPPFILES)
	#$(VPPDE)  -l -r $(VPPFILES)

# run VDMJ
vdmj:
	vdmj_UTF8 -r classic -exceptions -e "run()" $(VPPFILES)
	echo  "you have to type 'latex' and 'q'"
	vdmj_UTF8 -r classic -exceptions $(VPPFILES)

doc: #今は「! LaTeX Error: Environment vdm_al undefined.」というエラーが出る
	$(PLATEX) $(OUTDOC)
	$(BIBTEX) $(OUTDOC)
	makeindex $(OUTDOC).idx
	$(PLATEX) $(OUTDOC)
	$(PLATEX) $(OUTDOC)
	$(DVIPDFM) $(OUTDOC)
	

# To use the PNG file on TeX, *.bb is needed. 
makebb:
	cd $(IMGDIR); $(EBB) *.png
#	cd $(IMGDIR); $(EBB) *.pdf

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

