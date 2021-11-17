###########################
# Auto VDM -> TeX report
###########################

## Definitions
#################

#encode
#CODE = SJIS
CODE = UTF8

# TeX commands
TEXDIR = /usr/local/texlive/2021/bin/universal-darwin
PLATEX = $(TEXDIR)/platex --kanji=$(C0DE)
#BIBTEX=jbibtex
BIBTEX=pbibtex --kanji=$(C0DE)
DVIPDFM = $(TEXDIR)/dvipdfmx
EBB = ebb

# VDMTools command line
VPPDE = vppde

# Output document name
OUTDOC = GuardedCommand
MODELDOC = studyOfModel
USRMAN = HowToRun

# VDM files
VPPFILES = \
TestApp.vpp	BlackBoard.vpp	GuardedCommand_UserDoorClose.vpp \
Common.vpp					GuardedCommand_UserDoorOpen.vpp \
Door.vpp					GuardedCommand_UserGuidedMove.vpp \
Door_Real_Enter.vpp				GuardedCommand_UserMove.vpp \
Door_Real_Exit.vpp				Guide.vpp \
Door_Vairtual.vpp				IDCard.vpp \
GuardedCommand.vpp				IDTerminal.vpp \
GuardedCommand_Guide.vpp				LocationGraph.vpp \
GuardedCommand_IDTerminal.vpp			Object.vpp \
GuardedCommand_IDTerminal_Gamma_NG.vpp		Scheduler.vpp \
GuardedCommand_IDTerminal_Gamma_OK.vpp		Sensor.vpp \
GuardedCommand_IDTerminal_Gamma_OK_Virtual.vpp	\
GuardedCommand_IDTerminal_NG.vpp			TestCase.vpp \
GuardedCommand_IDTerminal_OK.vpp			TouchPanel.vpp \
GuardedCommand_IDTerminal_OK_Virtual.vpp		User.vpp \
GuardedCommand_Sensor.vpp			VDMUtil.vpp \
GuardedCommand_Sensor_Virtual.vpp		VPPUnit.vpp \
GuardedCommand_User.vpp				io.vpp \
GuardedCommand_UserCertified.vpp			math.vpp \
GuardedCommand_UserCertified_Virtual.vpp \


# Test script name
TESTSCRIPT = test.script
# Image directory
IMGDIR = image

## Make
#################

# make target
all: $(OUTDOC) $(MODELDOC) $(USRMAN)

$(OUTDOC): makebb makevdmtex
	$(PLATEX) $(OUTDOC)
	$(BIBTEX) $(OUTDOC) 
	makeindex  $(OUTDOC).idx
	$(PLATEX) $(OUTDOC)
	$(PLATEX) $(OUTDOC)
	$(DVIPDFM) $(OUTDOC)

$(MODELDOC):  makebb  
	$(PLATEX) $(MODELDOC)
	$(BIBTEX) $(MODELDOC) 
#	makeindex  $(OUTDOC).idx
	$(PLATEX) $(MODELDOC)
	$(PLATEX) $(MODELDOC)
	$(DVIPDFM) $(MODELDOC)

$(USRMAN):  makebb  
	$(PLATEX) $(USRMAN)
	$(BIBTEX) $(USRMAN) 
#	makeindex  $(OUTDOC).idx
	$(PLATEX) $(USRMAN)
	$(PLATEX) $(USRMAN)
	$(DVIPDFM) $(USRMAN)
	
# run VDMTools
makevdmtex:
	# Read & Syntax check
	LANG=ja_JP.$(CODE) $(VPPDE) -p -R vdm.tc $(VPPFILES)
	# Type check
	LANG=ja_JP.$(CODE) $(VPPDE) -t $(VPPFILES)
	# Run Interpreter with TESTSCRIPT
	#LANG=ja_JP.$(CODE) $(VPPDE) -i -D -I -P -Q -R vdm.tc $(TESTSCRIPT) $(VPPFILES)
	# Run Interpreter with "set exception" option
	LANG=ja_JP.$(CODE) time $(VPPDE) -y -i -D -I -P -Q -R vdm.tc $(TESTSCRIPT) $(VPPFILES)
	# Pretty print
	LANG=ja_JP.$(CODE) $(VPPDE)  -l -r $(VPPFILES)

# run VDMJ
vdmj:
	vdmj_UTF8 -r classic -exceptions -e "Execute()" $(VPPFILES)
	echo  "you have to type 'latex' and 'q'"
	vdmj_UTF8 -r classic -exceptions $(VPPFILES)

# To use the PNG file on TeX, *.bb is needed. 
makebb:
#	cd $(IMGDIR); $(EBB) *.png
	cd $(IMGDIR); $(EBB) *.pdf
	
# Clean files. But Output document is not deleted.
clean:
	rm -rf *.aux *.log *.bbl *.blg *.dvi *.toc
	rm -rf *.out *.vpp.tex *.vdmpp.tex *.idx vdm.tc
	rm -rf */*.aux */*.log */*.bbl */*.blg */*.dvi */*.toc
	rm -rf */*.out */*.vpp.tex */*.vdmpp.tex */*.idx */vdm.tc
	rm -rf generated/latex/specification/*.vpp.tex generated/latex/specification/*.vdmpp.tex 
	rm -rf generated/latex/*.log generated/latex/*.out generated/latex/*.aux generated/latex/*.toc

# Clean output document
realclean: clean
	rm -rf $(OUTDOC).pdf