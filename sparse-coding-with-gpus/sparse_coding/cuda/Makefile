# Author: Anand Madhavan

# NOTE: Please change these three..
CUDA_INC	:= /Developer/CUDA/common/inc
CUDA_LIB	:= /usr/local/cuda
CUDA_SDK_LIB  := $(CUDA_LIB)/sdk/lib
# change to point to local CUDA installations.

NVCC       := nvcc
CPP	       := g++
CUDA_INC_PATH  := -I. -I$(CUDA_INC)
CUDA_LIB_PATH  := -L$(CUDA_SDK_LIB) -L$(CUDA_LIB)/lib
NVCC_OPTIONS   := 
CPP_OPTIONS    := -fPIC -O3 
CUDA_LIBS      := -lcutil -lcudart -lcublas
TARGET		   := cl1ls

default: $(TARGET)

clean_intermediate:
	rm -f *.o *.cu_o

$(TARGET): *.cu *.cc *.hh Makefile
	$(NVCC) $(NVCC_OPTIONS) $(CUDA_INC_PATH) -o GPU.cu_o -c GPU.cu
	$(NVCC) $(NVCC_OPTIONS) $(CUDA_INC_PATH) -o main.cu_o -c main.cu
	$(NVCC) $(NVCC_OPTIONS) $(CUDA_INC_PATH) -o l1ls_coord_descent.cu_o -c l1ls_coord_descent.cu
	$(NVCC) $(NVCC_OPTIONS) $(CUDA_INC_PATH) -o proj_grad_descent.cu_o -c proj_grad_descent.cu
	$(CPP) $(CPP_OPTIONS) -o Matrix.o -c Matrix.cc
	$(CPP) $(CPP_OPTIONS) -o l1ls_coord_descent.o -c l1ls_coord_descent.cc
	$(CPP) $(CPP_OPTIONS) -o $(TARGET) GPU.cu_o main.cu_o Matrix.o l1ls_coord_descent.cu_o l1ls_coord_descent.o proj_grad_descent.cu_o $(CUDA_LIB_PATH) $(CUDA_LIBS) $(CPPUNIT_LIBS)
#	make clean_intermediate

clean:
	rm -f *.cu_o *.o *.prof *.ptx $(TARGET) 
