#-------------------------------------------------------------------------------
# SuiteSparse_GPURuntime/Lib/Makfile
#-------------------------------------------------------------------------------

include ../../SuiteSparse_config/SuiteSparse_config.mk

OBJS = SuiteSparseGPU_Workspace.o                     \
       SuiteSparseGPU_Workspace_cpuAllocators.o       \
       SuiteSparseGPU_Workspace_gpuAllocators.o       \
       SuiteSparseGPU_Workspace_transfer.o

INC = -I../Include -I../../SuiteSparse_config
LIBS = $(CUDART_LIB)

H = \
        ../Include/SuiteSparseGPU_Workspace.hpp \
        ../Include/SuiteSparseGPU_debug.hpp \
        ../Include/SuiteSparseGPU_macros.hpp \
        ../Include/SuiteSparseGPU_workspace_macros.hpp \
        ../Include/SuiteSparseGPU_Runtime.hpp \
        Makefile

#-------------------------------------------------------------------------------

all: runtime shared

library: runtime

lib: runtime

clean:
	$(RM) -f *.o

purge: clean
	$(RM) -f libSuiteSparse_GPURuntime.a libSuiteSparse_GPURuntime.so

runtime: $(OBJS)
	$(AR) -r "libSuiteSparse_GPURuntime.a" $(OBJS)

SuiteSparseGPU_Workspace.o: ../Source/SuiteSparseGPU_Workspace.cpp $(H)
	$(NVCC) -dc $(INC) $<

SuiteSparseGPU_Workspace_cpuAllocators.o: ../Source/SuiteSparseGPU_Workspace_cpuAllocators.cpp $(H)
	$(NVCC) -dc $(INC) $<

SuiteSparseGPU_Workspace_gpuAllocators.o: ../Source/SuiteSparseGPU_Workspace_gpuAllocators.cpp $(H)
	$(NVCC) -dc $(INC) $<

SuiteSparseGPU_Workspace_transfer.o: ../Source/SuiteSparseGPU_Workspace_transfer.cpp $(H)
	$(NVCC) -dc $(INC) $<


cuda_link_lib: $(OBJS)
	$(NVCC) $(INC) --shared -Xcompiler -fPIC -dlink $(OBJS) -o libSuiteSparse_GPURuntime_link.o

shared: cuda_link_lib
	$(CC) $(INC) -shared -o libSuiteSparse_GPURuntime.so \
		libSuiteSparse_GPURuntime_link.o -L../../lib -lsuitesparseconfig
