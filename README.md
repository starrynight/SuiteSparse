# SuiteSparse
SuiteSparse with CUDA solver and Metis 5.x, compiled as shared libraries for Julia

Top level makefile doesn't work. Test and demo don't work. Must cd in to each library to build the library files.
Only those libraries required by Julia have been modified.

## Prerequisite
1. Openblas has been installed within default library folder
2. Metis has been compiled as shared library (make config shared=1) and is copied to "lib" folder. 
    If using Metis 5.x, must apply patch on CHOLMOD/Partition/cholmod_metis.c, to replace 'idx_type' with 'idx_t'

Compileing sequence:
1. suitesparseconfig
2. AMD, CAMD, COLAMD, CCOLAMD
3. CHOLMOD
4. SPQR
5. UMFPack

Each library must be manually copied to the "lib" folder in the source directory for next step
