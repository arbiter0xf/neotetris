# NOTE:
# Currently `make clean` is required when switching build targets, i.e. first
# building 'debug', followed by 'release'.
#
# It might be possible to avoid requiring `make clean` in the middle. One way
# which comes to mind, is having a separate set of object files. Release build
# would then build .o files with different names, when compared to debug build.
# As in: 'local_ping.o' and 'local_ping_debug.o' for example.

SRC := $(wildcard *.c)
OBJ := $(SRC:.c=.o)

EXECUTABLE_PING_DEBUG := exe_ping_debug
EXECUTABLE_PONG_DEBUG := exe_pong_debug
EXECUTABLE_PING := exe_ping
EXECUTABLE_PONG := exe_pong
ALL_EXECUTABLES_DEBUG := \
	$(EXECUTABLE_PING_DEBUG) \
	$(EXECUTABLE_PONG_DEBUG)
ALL_EXECUTABLES_RELEASE := \
	$(EXECUTABLE_PING) \
	$(EXECUTABLE_PONG)
ALL_EXECUTABLES := \
	$(ALL_EXECUTABLES_DEBUG) \
	$(ALL_EXECUTABLES_RELEASE)

OBJ_PING := \
	local_ping.o \
	util.o
OBJ_PONG := \
	local_pong.o \
	util.o

MACRO_DEFINITIONS_RELEASE := -DNDEBUG

# Currently set empty macro definitions for debug target
MACRO_DEFINITIONS_DEBUG :=

# Temporarily uncomment the following row in order to debug.
# CFLAGS := -g $(CFLAGS)

ifeq ($(MAKECMDGOALS),release)
	MACRO_DEFINITIONS := $(MACRO_DEFINITIONS_RELEASE)
endif
ifeq ($(MAKECMDGOALS),debug)
	MACRO_DEFINITIONS := $(MACRO_DEFINITIONS_DEBUG)
endif
ifeq ($(MAKECMDGOALS),)
	# If no target given on commandline, expect defaulting to 'debug'
	# target.
	MACRO_DEFINITIONS := $(MACRO_DEFINITIONS_DEBUG)
endif

%.o : %.c
	$(CC) -c $(CFLAGS) $(MACRO_DEFINITIONS) $< -o $@

.PHONY: clean

debug: $(ALL_EXECUTABLES_DEBUG)

release: $(ALL_EXECUTABLES_RELEASE)

$(EXECUTABLE_PING_DEBUG): $(OBJ_PING)
	$(CC) $(CFLAGS) $(MACRO_DEFINITIONS) $^ -o $@

$(EXECUTABLE_PONG_DEBUG): $(OBJ_PONG)
	$(CC) $(CFLAGS) $(MACRO_DEFINITIONS) $^ -o $@

$(EXECUTABLE_PING): $(OBJ_PING)
	$(CC) $(CFLAGS) $(MACRO_DEFINITIONS) $^ -o $@

$(EXECUTABLE_PONG): $(OBJ_PONG)
	$(CC) $(CFLAGS) $(MACRO_DEFINITIONS) $^ -o $@

clean: $(ALL_EXECUTABLES) $(OBJ)
	$(RM) $^
