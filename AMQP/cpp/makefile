# 
# IPWorks IoT 2022 C++ Edition - Sample Project
# 
# This sample project demonstrates the usage of IPWorks IoT in a 
# simple, straightforward way. This is not intended to be a complete 
# application. Error handling and other checks are simplified for clarity.
# 
# Copyright (c) 2023 /n software inc. www.nsoftware.com
# 

ifeq ($(shell uname -s), Darwin) # MACOS
R_PATH=-Wl,-rpath,../../lib64/,-rpath,.

FRAMEWORK = -framework Carbon -framework Security
LD_FLAGS = -lipworksiot.22.0 -L../../lib64/ -lresolv
LD_FLAGS_SRC = -lz -lresolv
OS_CFLAGS = -D UNIX -arch arm64
MACOS = "darwin% Darwin% macos%"

all:
	g++ $(OS_CFLAGS) -D UNIX -o amqp amqp.cpp  -I../../include/ $(LD_FLAGS) $(FRAMEWORK) $(R_PATH)

src: ../../src/ipworksiot.o
	g++ $(OS_CFLAGS) -o amqp ../../src/ipworksiot.o amqp.cpp  $(LD_FLAGS_SRC) $(FRAMEWORK)

../../src/ipworksiot.o:
	g++ -c -fno-exceptions -fno-rtti -fPIC -arch arm64 -o ../../src/ipworksiot.o ../../src/ipworksiot.cpp

else # LINUX
ifeq ($(shell uname -m), x86_64)
  LIB=lib64
else
  LIB=lib
endif

R_PATH=-Wl,-rpath,../../$(LIB)/,-rpath,.
LD_FLAGS = -lipworksiot  -L../../$(LIB)/ 
LD_FLAGS_SRC = -lz 

all:
	g++ -D UNIX -o amqp amqp.cpp  -I../../include/ $(LD_FLAGS) $(R_PATH) 

src: ../../src/ipworksiot.o
	g++ -D UNIX -o amqp ../../src/ipworksiot.o amqp.cpp  -I../../include/ $(LD_FLAGS_SRC)

../../src/ipworksiot.o:
	g++ -c -fno-exceptions -fno-rtti -fPIC -o ../../src/ipworksiot.o ../../src/ipworksiot.cpp

clean:
	rm -f ../../src/*.o
	rm -f amqp *.o
endif