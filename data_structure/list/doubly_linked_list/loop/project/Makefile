#################################################
# 针对C环境,一个目录下所有.cpp编译出一个可执行文件,
# 编写的Makefile
#
# $@:   目标文件
# $^:   所有的依赖文件
# $<:   第一个依赖文件.
#
# author:       gaochao
# email:        gaoc@dsp.ac.cn
# date:         2009/03/24
#################################################

#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~#
#		 need complete
#
# {exe(default), static, shared}
BINARY_TYPE := 

MODULE := test

LFLAGS := 

CFLAGS := -Wall -MD -g -O2 
CFLAGS += 
#
#		     done
#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~#


ifeq ($(BINARY_TYPE), static)
	TARGET = $(addsuffix .a, $(addprefix lib, $(MODULE)))
else
ifeq ($(BINARY_TYPE), shared)
	TARGET = $(addsuffix .so, $(addprefix lib, $(MODULE)))
endif
endif

TARGET ?= $(MODULE)

.PHONY: all
all: createdir $(TARGET)
	#chmod a+x $(TARGET)
	@echo "-------- $(TARGET) done ---------"

SOURCES := $(wildcard *.cpp)

OBJS := $(patsubst %.cpp, %.o, $(SOURCES))

OBJDIR := .objs

CROSS_COMPILE := 

AS := $(CROSS_COMPILE)as
LD := $(CROSS_COMPILE)ld
CC := $(CROSS_COMPILE)gcc

CXX := $(CROSS_COMPILE)g++
AR := $(CROSS_COMPILE)ar

MKDIR := mkdir -p
RM := rm -rf

.PHONY: createdir
createdir: 
	$(MKDIR) $(OBJDIR)

%.o: %.cpp
	$(CXX) $(CFLAGS) -c $< -o $(OBJDIR)/$@ 

$(TARGET): $(OBJS)
ifeq ($(BINARY_TYPE), static)
	$(AR) rc $@ $(addprefix $(OBJDIR)/, $^)
else
ifeq ($(BINARY_TYPE), shared)
	$(CXX) -shared -o $@ $(addprefix $(OBJDIR)/, $^)
else
	$(CXX) -o $@ $(addprefix $(OBJDIR)/, $^) $(LFLAGS)
endif
endif

.PHONY: clean
clean:
	$(RM) $(TARGET)
	$(RM) $(OBJDIR)

