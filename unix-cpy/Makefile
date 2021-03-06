PYSRC=../py
BUILD=build

CC = gcc
CFLAGS = -I. -I$(PYSRC) -Wall -Werror -ansi -std=gnu99 -Os #-DNDEBUG
LDFLAGS = -lm

SRC_C = \
	main.c \

PY_O = \
	nlrx86.o \
	nlrx64.o \
	malloc.o \
	qstr.o \
	vstr.o \
	unicode.o \
	lexer.o \
	lexerunix.o \
	parse.o \
	scope.o \
	compile.o \
	emitcommon.o \
	emitpass1.o \
	emitcpy.o \
	runtime.o \
	map.o \
	obj.o \
	objbool.o \
	objboundmeth.o \
	objcell.o \
	objclass.o \
	objclosure.o \
	objcomplex.o \
	objdict.o \
	objexcept.o \
	objfloat.o \
	objfun.o \
	objgenerator.o \
	objinstance.o \
	objint.o \
	objlist.o \
	objmodule.o \
	objnone.o \
	objrange.o \
	objset.o \
	objslice.o \
	objstr.o \
	objtuple.o \
	objtype.o \
	builtin.o \
	builtinimport.o \
	vm.o \
	showbc.o \
	repl.o \

OBJ = $(addprefix $(BUILD)/, $(SRC_C:.c=.o) $(PY_O))
LIB =
PROG = cpy

$(PROG): $(BUILD) $(OBJ)
	$(CC) -o $@ $(OBJ) $(LIB) $(LDFLAGS)

$(BUILD):
	mkdir -p $@

$(BUILD)/%.o: %.c
	$(CC) $(CFLAGS) -c -o $@ $<

$(BUILD)/%.o: $(PYSRC)/%.S
	$(CC) $(CFLAGS) -c -o $@ $<

$(BUILD)/%.o: $(PYSRC)/%.c mpconfigport.h
	$(CC) $(CFLAGS) -c -o $@ $<

$(BUILD)/emitnx64.o: $(PYSRC)/emitnative.c $(PYSRC)/emit.h
	$(CC) $(CFLAGS) -DN_X64 -c -o $@ $<

$(BUILD)/emitnthumb.o: $(PYSRC)/emitnative.c $(PYSRC)/emit.h
	$(CC) $(CFLAGS) -DN_THUMB -c -o $@ $<

# optimising vm for speed, adds only a small amount to code size but makes a huge difference to speed (20% faster)
$(BUILD)/vm.o: $(PYSRC)/vm.c
	$(CC) $(CFLAGS) -O3 -c -o $@ $<

$(BUILD)/main.o: mpconfigport.h
$(BUILD)/parse.o: $(PYSRC)/grammar.h
$(BUILD)/compile.o: $(PYSRC)/grammar.h
$(BUILD)/emitcpy.o: $(PYSRC)/emit.h
$(BUILD)/emitbc.o: $(PYSRC)/emit.h

clean:
	/bin/rm -rf $(BUILD)

.PHONY: clean
