#===================================================
# GNUmakefile for GCC 4.01							
# S.R.K. Branavan									
# Massachusetts Institute of Technology				
#===================================================


# flags --------------------------------------------
CC=	g++
RM=	rm 
SHARED_OBJECT_FLAG = -shared
INC_PATH = ../../include
LIB_PATH = ../../../lib

DEBUG = -ggdb -pg
OPTIMIZE = -fno-rtti -O3 -pg
LARGE_FILE_SUPPORT = -D_FILE_OFFSET_BITS=64 -D_LARGEFILE_SOURCE

INTEL_OPT_FLAGS = -mtune=native -march=native -mfpmath=sse -msse2
INTEL64_OPT_FLAGS = -mtune=native -march=native -mfpmath=sse -msse4 -m64 -fPIC
AMD_OPT_FLAGS = -mtune=opteron -march=opteron -mfpmath=sse -m3dnow -fPIC


# set debug & optimization flags...	----------------
CXXFLAGS = -I$(INC_PATH) \
		   -Wall \
		   $(OPTIMIZE) \
		   $(INTEL_OPT_FLAGS) \
		   $(LARGE_FILE_SUPPORT) \
		   -fPIC


# build targets  -----------------------------------
# the default build target here is lib				

TARGET = libnlp_string.so
MASTER_INCLUDE = nlp_string.h PorterStemmer.h
OBJS = StringBase.o StringFind.o StringOperators.o StringAdv.o PorterStemmer.o


ifeq (test,$(MAKECMDGOALS))
	TARGET = strtest
	OBJS = main.o
	LIBS = -lnlp_string
endif




# build commands -----------------------------------
.PHONY : all auto build clean install test

auto: build install

all: clean build

test: clean build

build: $(OBJS)
	$(CXX) -L$(LIB_PATH) -o$(TARGET) $(DEBUG) $(SHARED_OBJECT_FLAG) $(OBJS) $(LIBS)

install:
	install -d $(INC_PATH)
	install -m0644 $(MASTER_INCLUDE) $(INC_PATH)
	install -d $(LIB_PATH)
	install -m0644 $(TARGET) $(LIB_PATH)

clean:
	@echo "  -- cleaning out object files : " $(TARGET)  $(OBJS)
	-@$(RM) -f $(OBJS) $(TARGET)

