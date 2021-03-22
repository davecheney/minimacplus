#Makefile for a native (SDL) tme build

TARGET:=tme
MUSASHI_GEN_SRC:=musashi/m68kops.c
OBJ:=$(MUSASHI_GEN_SRC:%.c=%.o) musashi/m68kcpu.o musashi/softfloat/softfloat.o \
	sdl/main.o sdl/disp.o sdl/hd.o sdl/snd.o \
	emu.o iwm.o via.o rtc.o ncr.o scc.o mouse.o hexdump.o \
	network/localtalk.o network/ddp.o network/ethertalk.o network/basiliskif.o network/sniff.o
#musashi/m68kdasm.o
CFLAGS=-Wall -I. -I./musashi -I./hostbuild -I/opt/local/include -O3 -ggdb `sdl2-config --cflags` -DHOSTBUILD -DMUSASHI_CNF=\"m68kconf.h\" 
LDFLAGS=`sdl2-config --libs` -lm

$(TARGET): $(OBJ)
	$(CC) -o $(@) $(CFLAGS) $(LDFLAGS) $^

$(MUSASHI_GEN_SRC): musashi/m68kmake
	cd musashi; ../$(^)

$(MUSASHI_OP_PREGEN_SRC): $(MUSASHI_GEN_SRC)
	$(CC) -o musashi/m68kops musashi/m68kops.c
	./musashi/m68kops > $(MUSASHI_OP_PREGEN_SRC)

musashi/m68kmake: musashi/m68kmake.c
	$(CC) -o $@ $^

clean:
	rm -f $(MUSASHI_GEN_SRC) musashi/m68kmake
	rm -f $(OBJ) $(TARGET)
