.SUFFIXES: .c .o

CC=gcc

SRC_DIR=src/
INC=include/
LIBS=lib/

# SRCS:=$(wildcard src/*.c)
# OBJS:=$(SRCS:.c=.o)

# main source file
TARGET_SRC:=$(SRC_DIR)main.c
TARGET_OBJ:=$(SRC_DIR)main.o

OBJECTS = $(SRC_DIR)main.o $(SRC_DIR)buffer.o $(SRC_DIR)file.o $(SRC_DIR)bpt.o

# Include more files if you write another source file.
SRCS_FOR_LIB:=$(SRC_DIR)bpt.c $(SRC_DIR)file.c $(SRC_DIR)buffer.c
OBJS_FOR_LIB:=$(SRCS_FOR_LIB:.c=.o)

CFLAGS+= -g -fPIC -I $(INC)

TARGET=$(SRC_DIR)main
DATAFILE = $(SRC_DIR)table

all: $(TARGET)

$(TARGET): $(OBJECTS)
	$(CC) $(CFLAGS) -o $@ $(OBJECTS)
	make static_library
	$(CC) $(CFLAGS) -o $@ $^ -L $(LIBS) -lbpt

clean:
	rm $(TARGET) $(OBJECTS) $(LIBS)*
	rm $(DATAFILE)*

library:
	gcc -shared -Wl,-soname,libbpt.so -o $(LIBS)libbpt.so $(OBJS_FOR_LIB)

# make static library libbpt.a using following object files
static_library:
	ar cr $(LIBS)libbpt.a $(OBJS_FOR_LIB)


# dependency
# bpt.h, file.h and buffer.h include ptype.h! -> is new dependency needed? -> no
$(SRC_DIR)bpt.o : $(SRC_DIR)bpt.c $(INC)bpt.h $(INC)file.h $(INC)buffer.h $(INC)table.h 
$(SRC_DIR)file.o : $(SRC_DIR)file.c $(INC)file.h $(INC)table.h
$(SRC_DIR)buffer.o : $(SRC_DIR)buffer.c $(INC)buffer.h $(INC)file.h $(INC)table.h
$(SRC_DIR)main.o : $(SRC_DIR)main.c $(INC)bpt.h $(INC)buffer.h
