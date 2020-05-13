CXX		  := g++
CXX_FLAGS := -Wall -Wextra -std=c++17 -ggdb

EXEC 	:= main
BIN		:= bin
SRC		:= src
OBJ		:= obj
INCLUDE	:= include
LIB		:= lib

LIBRARIES	:=

ifeq ($(OS),Windows_NT)
EXECUTABLE	:= $(EXEC).exe
INCLUDEDIRS	:= $(INCLUDE)
LIBDIRS		:= $(LIB)
else
EXECUTABLE	:= $(EXEC)
INCLUDEDIRS	:= $(shell find $(INCLUDE) -type d)
LIBDIRS		:= $(shell find $(LIB) -type d)
endif

CINCLUDES	:= $(patsubst %,-I%, $(INCLUDEDIRS:%/=%))
CLIBS		:= $(patsubst %,-L%, $(LIBDIRS:%/=%))

SOURCES		:= main.cpp $(wildcard $(SRC)/*.cpp)
OBJECTS		:= $(SOURCES:%.cpp=$(OBJ)/%.o)

all: $(BIN)/$(EXECUTABLE)

run: clean all
	clear
	./$(BIN)/$(EXECUTABLE)

$(BIN)/$(EXECUTABLE): $(OBJECTS)
	$(CXX) -o $@ $^

$(OBJ)/%.o: %.cpp
	test -d $(@D) || @mkdir -p $(@D)
	$(CXX) $(CXX_FLAGS) $(CINCLUDES) $(CLIBS) -c -o $@ $< $(LIBRARIES)

.PHONY: clean
clean:
	-$(RM) $(BIN)/*
	-$(RM) $(OBJECTS)
