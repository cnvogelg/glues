# Linux Makefile for glues

# RaspberryPi Raspbian compatible compile
ifeq ($(raspi),1)
CFLAGS += -I$(RASPI_ROOT)/opt/vc/include # location of GLES headers
CFLAGS += -march=armv6 -mfloat-abi=hard -mfpu=vfp 
endif

cc=$(COMPILER_PREFIX)$(CC)
ar=$(COMPILER_PREFIX)$(AR)

SRCS = glues_error.c glues_mipmap.c glues_project.c glues_quad.c glues_registry.c
TESS_SRCS = dict.c geom.c memalloc.c mesh.c normal.c priorityq.c render.c sweep.c tess.c tessmono.c
OBJS = $(patsubst %.c,%.o,$(SRCS))
OBJS += $(patsubst %.c,%.o,$(TESS_SRCS))
VPATH = ../source:../source/libtess
CFLAGS += -I../source
LDFLAGS += -shared
LIB_NAME = libGLUES.a
INSTALL_PREFIX = ..

.PHONY: all install clean

all: $(LIB_NAME)

install: all
	mkdir -p $(INSTALL_PREFIX)/include/GLES
	mkdir -p $(INSTALL_PREFIX)/lib
	cp $(LIB_NAME) $(INSTALL_PREFIX)/lib
	cp ../source/glues.h $(INSTALL_PREFIX)/include/GLES/glu.h

clean:
	rm -f $(OBJS) $(LIB_NAME)
	rm -f $(INSTALL_PREFIX)/include/glu.h $(INSTALL_PREFIX)/include/glues.h
	rm -f $(INSTALL_PREFIX)/lib/$(LIB_NAME)

$(LIB_NAME): $(OBJS)
	$(ar) cru $@ $(OBJS)

$(OBJS): $(SRCS)

%.o: %.c
	$(cc) $(CFLAGS) -c $< -o $@
