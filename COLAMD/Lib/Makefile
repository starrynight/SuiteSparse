#-------------------------------------------------------------------------------
# COLAMD Makefile
#-------------------------------------------------------------------------------

default: libcolamd.a libcolamd.so

include ../../SuiteSparse_config/SuiteSparse_config.mk

I = -I../Include -I../../SuiteSparse_config

INC = ../Include/colamd.h ../../SuiteSparse_config/SuiteSparse_config.h

SRC = ../Source/colamd.c

# creates libcolamd.a, a C-callable COLAMD library
libcolamd.a:  $(SRC) $(INC)
	$(CC) $(CF) $(I) -c ../Source/colamd.c
	$(CC) $(CF) $(I) -c ../Source/colamd.c -DDLONG -o colamd_l.o
	$(ARCHIVE)  libcolamd.a colamd.o colamd_l.o
	- $(RANLIB) libcolamd.a

libcolamd.so:
	$(CC) -shared -o libcolamd.so colamd.o colamd_l.o -L../../lib -lsuitesparseconfig

ccode: libcolamd.a

library: libcolamd.a

clean:
	- $(RM) $(CLEAN)

purge: distclean

distclean: clean
	- $(RM) libcolamd.a libcolamd.so
