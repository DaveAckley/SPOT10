NAME:=$(notdir $(realpath ..))
THIS_DIR:=$(strip $(notdir $(shell dirname $(realpath $(lastword $(MAKEFILE_LIST))))))
MFZ:=../$(NAME).mfz
# Customize ULAM_BIN_DIR and MFM_BIN_DIR if necessary
#ULAM_BIN_DIR:=/usr/bin
#MFM_BIN_DIR:=/usr/bin
ULAM_BIN_DIR:=$(realpath ../../ULAM/bin)
MFM_BIN_DIR:=$(realpath ../../MFM/bin)
ULAM:=$(ULAM_BIN_DIR)/ulam
MFZRUN:=$(MFM_BIN_DIR)/mfzrun
#UFLAGS:=-g
#UFLAGS:=--sa
UFLAGS:=-o
ARGS_TXT_FILES:=$(wildcard args.txt)
ULAM_FILES:=$(wildcard *.ulam)
INC_FILES:=$(wildcard *.inc)
MFS_FILES:=$(wildcard *.mfs)
TIMESTAMP:=$(shell date +%Y%m%d-%H%M%S)
DEV:=$(shell whoami)
ISHNAME:=$(TIMESTAMP)-$(DEV)
MFZARGS:=

all:	$(MFZ)

run:	$(MFZ)
	$(MFZRUN) $(MFZ) run $(MFZARGS)

$(MFZ):	$(ULAM_FILES) $(ARGS_TXT_FILES) Makefile
	$(ULAM) $(UFLAGS) $(ULAM_FILES) $(INC_FILES) $(MFS_FILES) $(ARGS_TXT_FILES) $(MFZ)

clean:
	rm -f *~
	rm -rf .gen

realclean: clean
	rm -f $(MFZ)

ishtar:
	@make clean
	@make >ISH-BUILD-STDOUT.txt 2>ISH-BUILD-STDERR.txt || true
	@cd ..;tar cvzf $(ISHNAME).tgz $(THIS_DIR) --transform s/^$(THIS_DIR)/$(ISHNAME)/
	@echo Made ../$(ISHNAME).tgz

.PHONY:	all mfz clean realclean tar ishtar

