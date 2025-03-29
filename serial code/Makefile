# CC=gcc
# LIBS= 
# SOURCE_DIR= .
# BIN_DIR= .
# CFLAGS= -O1 -g
# LDFLAGS= -lm 
# OBJS=$(SOURCE_DIR)/canny_edge.o $(SOURCE_DIR)/hysteresis.o $(SOURCE_DIR)/pgm_io.o
# EXEC= canny
# INCS= -I.
# CSRCS= $(SOURCE_DIR)/canny_edge \
# 	$(SOURCE_DIR)/hysteresis.c \
# 	$(SOURCE_DIR)/pgm_io.c

# # PIC=pics/pic_small.pgm
# # PIC=pics/pic_medium.pgm
# PIC=pics/pic_large.pgm

# all: canny

# canny: $(OBJS)
# 	$(CC) $(CFLAGS)  -o $@ $? $(LDFLAGS)

# %.o: %.c
# 	$(CC) $(CFLAGS) -c $< -o $@

# run: $(EXEC) $(PIC)
# 	./$(EXEC) $(PIC) 2.5   0.25  0.5
# # 			        sigma tlow  thigh

	

# gprof:	CFLAGS +=  -pg
# gprof:  LDFLAGS += -pg 
# gprof:	clean all
# 	echo "./$(EXEC) $(PIC) 2.0 0.5 0.5" > lastrun.binary
# 	./$(EXEC) $(PIC) 2.0 0.5 0.5
# 	gprof -b ./$(EXEC) > gprof_$(EXEC).txt
# 	./run_gprof.sh canny


# clean:
# 	@-rm -rf canny $(OBJS) gmon.out

# .PHONY: clean comp exe run all


# Define variables
CC=gcc
NVCC=nvcc  # Use nvcc for CUDA compilation
LIBS=
SOURCE_DIR=.
BIN_DIR=.
CFLAGS=-O1 -g
LDFLAGS=-lm
OBJS=$(SOURCE_DIR)/kernals.o  # Updated object file
EXEC=canny
INCS=-I.

# Input image (use the large picture by default)
PIC=pics/pic_small.pgm

# Compilation rules
all: canny

# Link the object file to create the executable
canny: $(OBJS)
	$(NVCC) $(CFLAGS) -o $@ $? $(LDFLAGS)

# Compile CUDA source file to object file
$(SOURCE_DIR)/kernals.o: $(SOURCE_DIR)/parallerKernal.cu
	$(NVCC) $(CFLAGS) -c $< -o $@

# Run the executable with the picture
run: $(EXEC) $(PIC)
	./$(EXEC) $(PIC) 2.5 0.25 0.5

# gprof profiling (Note: CUDA profiling is handled differently using `nvprof` or `nsys`)
gprof: CFLAGS += -pg
gprof: LDFLAGS += -pg
gprof: clean all
	echo "./$(EXEC) $(PIC) 2.0 0.5 0.5" > lastrun.binary
	./$(EXEC) $(PIC) 2.0 0.5 0.5
	gprof -b ./$(EXEC) > gprof_$(EXEC).txt
	./run_gprof.sh canny

# Clean the build
clean:
	@-rm -rf canny $(OBJS) gmon.out

.PHONY: clean comp exe run all

