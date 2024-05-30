# TOOL VAR 
CC = gcc 
CFLAGS =
DEBUGFLAGS = -g
COMPFLAGS = -c 

# PATH VAR
BIN_PATH := ./bin
OBJ_PATH := ./obj
SRC_PATH := ./src
DBG_PATH := ./debug

# COMPILE VAR 
# CHECK OS FIRST
TARGET_NAME := main
ifeq ($(OS), Windows_NT)
	TARGET_NAME := $(addsuffix .exe,$(TARGET_NAME))
endif
TARGET := $(BIN_PATH)/$(TARGET_NAME)
TARGET_DEBUG := $(DBG_PATH)/$(TARGET_NAME)

# FILES 
SRC := $(wildcard $(addprefix $(SRC_PATH)/*, .c)) # all *.c files in ./src 
OBJ := $(addprefix $(OBJ_PATH)/, $(addsuffix .o, $(notdir $(basename $(SRC))))) #basename remove file extension -> "not dir" remove path -> add .o suffix -> add OBJ_PATH
OBJ_DEBUG := $(addprefix $(DBG_PATH)/, $(addsuffix .o, $(notdir $(basename $(SRC)))))
# CLEAN folder 
CLEAN_LIST := $(OBJ) $(TARGET) $(OBJ_DEBUG) $(TARGET_DEBUG)


# COMPILE 
$(TARGET): $(OBJ) #link
	$(CC) -o $@ $^ $(CFLAGS)

$(OBJ_PATH)/%.o: $(SRC_PATH)/%.c #compile .c -> .o 
	$(CC) -c $^ -o $@ $(CFLAGS)

# DEBUG 
$(TARGET_DEBUG): $(OBJ_DEBUG)
	$(CC) -o $@ $^ $(CFLAGS) $(DEBUGFLAGS)

$(DBG_PATH)/%.o: $(SRC_PATH)/%.c 
	$(CC) -c $^ -o $@ $(CFLAGS) $(DEBUGFLAGS)


.PHONY: makedir
makedir:
	@mkdir -p $(BIN_PATH) $(OBJ_PATH) $(DBG_PATH)

.PHONY: all
all: $(TARGET)

.PHONY: debug
debug: $(TARGET_DEBUG)

.PHONY: clean
clean:
	@echo CLEAN $(CLEAN_LIST)
	@rm -f $(CLEAN_LIST)
