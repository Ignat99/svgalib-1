#----------------------------------------------------------------------
# Makefile for SVGAlib demo programs.
#
# This file is a part of SVGAlib.
#----------------------------------------------------------------------

include ../Makefile.cfg

srcdir    = ..
VPATH     = $(srcdir)/demos

#----------------------------------------------------------------------
# Compiler Section (overrides Makefile.cfg)
#----------------------------------------------------------------------

CFLAGS = $(WARN) $(OPTIMIZE) -I$(srcdir)/include -I$(srcdir)/gl $(DEBFLAGS)
ifeq (a.out, $(TARGET_FORMAT))
  CFLAGS += -DSVGA_AOUT
endif

#----------------------------------------------------------------------
# Rules Section
#----------------------------------------------------------------------

PROGS    = fun testgl speedtest mousetest vgatest scrolltest testlinear \
	   keytest testaccel accel forktest eventtest spin bg_test printftest \
	   joytest mjoytest bankspeed lineart linearspeed addmodetest \
	   svidtune linearfork cursor vgatweak buildcsr

# Determine what library (static or shared) we will be linking programs with
ifdef INSTALLSHAREDLIB
  LIBS = -lvgagl -lvga
endif
ifndef LIBS
  LIBS    = ../staticlib/libvgagl.a ../staticlib/libvga.a -lm
  LVGADEP = $(LIBS)
endif

all:	$(PROGS) graphics

.PHONY: all clean cleanbin dep

$(PROGS): $(LVGADEP)

.c:
	$(CC) $(CFLAGS) $(LDFLAGS) -o $* $*.c $(LIBS) -L$(srcdir)/sharedlib
	$(INSTALL_PROGRAM) $* $(docdir)/demos/svgalib

rwpage: rwpage.pp
	$(PC) -Rintel rwpage.pp

testaccel: testaccel.c
	$(CC) $(CFLAGS) $(LDFLAGS) -o testaccel testaccel.c $(LIBS) -lm -L$(srcdir)/sharedlib
	$(INSTALL_PROGRAM) testaccel $(docdir)/demos/svgalib

accel: accel.c
	$(CC) $(CFLAGS) $(LDFLAGS) -o accel accel.c $(LIBS) -lm -L$(srcdir)/sharedlib
	$(INSTALL_PROGRAM) accel $(docdir)/demos/svgalib

linearspeed: linearspeed.c memset.o
	$(CC) $(CFLAGS) $(LDFLAGS) -o linearspeed linearspeed.c memset.o $(LIBS) -L$(srcdir)/sharedlib
	$(INSTALL_PROGRAM) linearspeed $(docdir)/demos/svgalib

buildcsr: mkcur.o
	$(CC) -o buildcsr $(LDFLAGS) mkcur.o -lvgagl -lvga -L$(srcdir)/sharedlib
	$(INSTALL_PROGRAM) buildcsr $(docdir)/demos/svgalib

graphics:
	$(INSTALL_DATA) linuxlogo.bitmap eightbpp.xbm clut.xbm sixbpp.xbm \
	wizard.xbm wizardmsk.xbm rwpage.pp $(docdir)/demos/svgalib

clean:	cleanbin
	rm -f .depend *.o *~ *.bak core

cleanbin:
	rm -f $(PROGS) rwpage

#
# No dependencies required here.
#

dep:
.depend:

