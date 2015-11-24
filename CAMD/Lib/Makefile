#-------------------------------------------------------------------------------
# CAMD Makefile for compiling on Unix systems (for GNU make only)
#-------------------------------------------------------------------------------

default: libcamd.a libcamd.so

include ../../SuiteSparse_config/SuiteSparse_config.mk

C = $(CC) $(CF) -I../Include -I../../SuiteSparse_config

#-------------------------------------------------------------------------------
# source files
#-------------------------------------------------------------------------------

CAMD = camd_aat camd_1 camd_2 camd_dump camd_postorder camd_defaults \
	camd_order camd_control camd_info camd_valid camd_preprocess

INC = ../Include/camd.h ../Include/camd_internal.h \
      ../../SuiteSparse_config/SuiteSparse_config.h

#-------------------------------------------------------------------------------
# object files for each version
#-------------------------------------------------------------------------------

CAMDI = $(addsuffix .o, $(subst camd_,camd_i_,$(CAMD)))
CAMDL = $(addsuffix .o, $(subst camd_,camd_l_,$(CAMD)))

#-------------------------------------------------------------------------------
# compile each int and long routine (with no real/complex version)
#-------------------------------------------------------------------------------

camd_i_%.o: ../Source/camd_%.c $(INC)
	$(C) -DDINT -c $< -o $@

camd_l_%.o: ../Source/camd_%.c $(INC)
	$(C) -DDLONG -c $< -o $@

#-------------------------------------------------------------------------------
# Create the libcamd.a library (C versions only)
#-------------------------------------------------------------------------------

libcamd.a: $(CAMDI) $(CAMDL)
	$(ARCHIVE)  libcamd.a $^
	- $(RANLIB) libcamd.a



libcamd.so: $(CAMDI) $(CAMDL)
	$(C) -shared -o libcamd.so $^ -L../../lib -lsuitesparseconfig


#-------------------------------------------------------------------------------
# Remove all but the files in the original distribution
#-------------------------------------------------------------------------------

clean:
	- $(RM) $(CLEAN)

purge: distclean

distclean: clean
	- $(RM) libcamd.a libcamd.so
