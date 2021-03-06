# Simple SDL mini Makefile

CC=gcc

CPPFLAGS= -MMD
CFLAGS= -Wall -Wextra -std=c99 -O3 -lm
LDFLAGS=
LDlib=

HEADERS= -Isrc -Isrc/Dataset -Isrc/Globals -Isrc/Network -Isrc/Predictions -Isrc/Training
SDLFLAGS = `sdl2-config --libs --cflags`


lib: src/Globals/Functions.c src/Dataset/Dataset.c src/Network/Network.c src/Network/IONetwork.c src/Predictions/Predict.c src/Training/Environment.c
	mkdir -p bin include lib
	${CC} -c -o lib/globals.o ${HEADERS} src/Globals/Functions.c ${CFLAGS}
	${CC} -c -o lib/dataset.o ${HEADERS} src/Dataset/Dataset.c ${CFLAGS}
	${CC} -c -o lib/network.o ${HEADERS} src/Network/Network.c ${CFLAGS}
	${CC} -c -o lib/ionetwork.o ${HEADERS} src/Network/IONetwork.c ${CFLAGS}
	${CC} -c -o lib/predict.o ${HEADERS} src/Predictions/Predict.c ${CFLAGS}
	${CC} -c -o lib/train.o ${HEADERS} src/Training/Train.c ${CFLAGS}
	${CC} -c -o lib/environment.o ${HEADERS} src/Training/Environment.c ${CFLAGS}
	${LD} -r -o lib/LambdaNeuralNetwork.o lib/globals.o lib/dataset.o lib/network.o lib/ionetwork.o lib/predict.o lib/train.o lib/environment.o
	cp src/*/*.h include/
	cp src/*.h include/
	
shared: lib
	${CC} -o lib/LambdaNeuralNetwork.so lib/LambdaNeuralNetwork.o ${SDLFLAGS} ${CFLAGS} -fPIC -shared


analyze: lib src/Executables/Analyze.c
	${CC} -o bin/analyze ${HEADERS} lib/LambdaNeuralNetwork.o src/Executables/Analyze.c ${SDLFLAGS} ${CFLAGS}

learning: lib src/Executables/Learning.c
	${CC} -o bin/learning ${HEADERS} lib/LambdaNeuralNetwork.o src/Executables/Learning.c ${SDLFLAGS} ${CFLAGS}

xor: lib src/Executables/XOR.c
	${CC} -o bin/xor ${HEADERS} lib/LambdaNeuralNetwork.o src/Executables/XOR.c ${SDLFLAGS} ${CFLAGS}

all: analyze learning xor


clean:
	rm -r lib bin include

# END

