#-------------------------------------------------------------------------------
# CCOLAMD Makefile
#-------------------------------------------------------------------------------

default: libccolamd.a libccolamd.so

include ../../SuiteSparse_config/SuiteSparse_config.mk

I = -I../Include -I../../SuiteSparse_config

INC = ../Include/ccolamd.h ../../SuiteSparse_config/SuiteSparse_config.h

SRC = ../Source/ccolamd.c

# creates libccolamd.a, a C-callable COLAMD library
libccolamd.a:  $(SRC) $(INC)
	$(CC) $(CF) $(I) -c ../Source/ccolamd.c
	$(CC) $(CF) $(I) -c ../Source/ccolamd.c -DDLONG -o ccolamd_l.o
	$(ARCHIVE)  libccolamd.a ccolamd.o ccolamd_l.o
	- $(RANLIB) libccolamd.a 


libccolamd.so: 
	$(CC) $(CF) $(I) -shared -o libccolamd.so ccolamd.o ccolamd_l.o \
		-L../../lib -lsuitesparseconfig

ccode: libccolamd.a

library: libccolamd.a

clean:
	- $(RM) $(CLEAN)

purge: distclean

distclean: clean
	- $(RM) libccolamd.a libccolamd.so
