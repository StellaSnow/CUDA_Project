CUDA_PATH 		:= /usr/local/cuda-8.0
TARGET_SIZE 	:= 64
HOST_COMPLIER 	:= g++
NVCC			:= $(CUDA_PATH)/bin/nvcc -ccbin $(HOST_COMPLIER)

NVCCFLAG		:= -m$(TARGET_SIZE)

SMS ?= 30 35 37 50 52 60 
GENCODE_FLAGS :=
$(foreach sm,$(SMS),$(eval GENCODE_FLAGS += -gencode arch=compute_$(sm),code=sm_$(sm)))


INCLUDE := -I /usr/local/include -I /usr/local/include/opencv -I /usr/local/include/opencv2 -I/usr/local/cuda-8.0/include
#INCLUDE += ${shell pkg-config  --libs opencv}



LIBS	:=
LIBS	+= -lopencv_core -lopencv_highgui -lopencv_imgproc
LIBS 	+= -L/usr/local/lib
LIBS 	+= -L/usr/local/cuda-8.0/lib64
LIBS 	+= -lcudart
LIBS 	+= -lcufft
#LIBS	+= -L/usr/local/Qt5.8.0/5.8/gcc_64/lib

CU_FILE := imregionmax.cu
CU_OBJ  += imregionmax.o
TARGET 	:= findpeeks
all:
	$(NVCC) $(GENCODE_FLAGS) $(NVCCFLAG) $(INCLUDE) $(LIBS) -c $(CU_OBJ)  $(CU_FILE)
	g++ main.cpp $(CU_OBJ) -o $(TARGET) $(INCLUDE) $(LIBS)

run:all 

	./$(TARGET)
clean:
	rm $(CU_OBJ) $(TARGET)

