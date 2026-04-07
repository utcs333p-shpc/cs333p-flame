BLIS_INSTALL_DIR     := $(HOME)/blis                                                
LIBFLAME_INSTALL_DIR := $(HOME)/libflame                                                
                                                                                
-include path.mk     


BLAS_LIB   := $(BLIS_INSTALL_DIR)/lib/libblis.a
FLAME_LIB  := $(LIBFLAME_INSTALL_DIR)/lib/libflame.a
FLAME_INC  := $(LIBFLAME_INSTALL_DIR)/include/

# indicate where the object files are to be created
CC         := gcc
LINKER     := $(CC)
CFLAGS     := -O3 -Wall -I$(FLAME_INC) -I$(CBLAS_INC) -m64 -march=native
FFLAGS     := $(CFLAGS) 

# set the range of experiments to be performed
NREPEATS   := 3#       number of times each experiment is repeated.
NFIRST     := 100#     smallest size to be timed.
NLAST      := 1500#    largest size to be timed.
NINC       := 100#     increment between sizes.

LDFLAGS    := -m64 -lm -fopenmp

# indicate where the FLAME include files reside

# add files in which your implementations are coded
TEST_OBJS  := driver.o symv_unb_var4.o

driver: $(TEST_OBJS) 
	$(LINKER) $(TEST_OBJS) $(FLAME_LIB) $(BLAS_LIB) $(LDFLAGS) -o driver.x

test:   driver
	echo "$(NREPEATS) $(NFIRST) $(NLAST) $(NINC)" | ./driver.x > output.m

%.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f *.o *~ core *.x output.m
