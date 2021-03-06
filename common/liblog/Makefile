# #All rights reserved.
# #
# ##Redistribution and use in source and binary forms, with or without modification,
# #are permitted provided that the following conditions are met:
# #
# ##1. Redistributions of source code must retain the above copyright notice, this
# #list of conditions and the following disclaimer.
# #
# ##2. Redistributions in binary form must reproduce the above copyright notice,
# #this list of conditions and the following disclaimer in the documentation
# #and/or other materials provided with the distribution.
# #
# ##3. Neither the name of the copyright holder nor the names of its contributors
# #may be used to endorse or promote products derived from this software without
# #specific prior written permission.
# #
# ##THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
# #ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
# #WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
# #DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
# #FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
# #DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
# #SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
# #CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
# #OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
# #OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
# #--------------------------------------------------------------------------***
# Read values from ones exported in master Makefile. Or, override on the command
# line if building separately.

TOPDIR?=$(shell pwd)/../..
include $(TOPDIR)/rules.mk

NAME:=log
TARGETS:=lib$(NAME).a

OBJECTS:=$(patsubst src/%.cpp,src/%.o,$(wildcard src/*.cpp))
OBJECTS:= $(OBJECTS) $(patsubst src/%.c,src/%.o,$(wildcard src/*.c))

CXXFLAGS+=-D$(DEBUG_CTL) -DRDMA_LL=$(LOG_LEVEL)
CXXFLAGS+=-I../../fabric_management/librio/inc


.PHONY: all clean test

all: $(TARGETS)

%.a: $(OBJECTS)
	@echo ---------- Building $@
	$(AR) rcs $@ $^

src/%.o:src/%.c
	@echo ---------- Building $@
	$(CXX) -c $(CXXFLAGS) $< -o $@

src/%.o:src/%.cpp
	@echo ---------- Building $@
	$(CXX) -c $(CXXFLAGS) $< -o $@

clean:
	@echo ---------- Cleaning lib$(NAME)...
	rm -f $(TARGETS) $(OBJECTS) \
	inc/*~ src/*~ *~
