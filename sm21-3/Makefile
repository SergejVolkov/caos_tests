CC = gcc

ifeq ($(MODE), release)
CFLAGS = -O2
else
CFLAGS = -Wall -Werror -g
endif

ifeq ($(LIB), math)
MFLAGS = -lm
endif

ifeq ($(SAN), true)
SFLAGS = -fsanitize=address
endif

ALLFLAGS = $(CFLAGS) $(SFLAGS) $(MFLAGS) -pthread -std=gnu11 -D_GNU_SOURCE -m32

SOURCE=$(wildcard *.c)
TARGET=main

all: $(TARGET)

include deps.make

$(TARGET) : $(SOURCE)
	$(CC) $(ALLFLAGS) $^ -o$@

clean:
	-rm -f $(TARGET) *.o deps.make

deps.make : $(SOURCE)
	gcc -MM $(SOURCE) > deps.make

runtests : $(TARGET)
	cd tests; ../run.sh ../$(TARGET)

