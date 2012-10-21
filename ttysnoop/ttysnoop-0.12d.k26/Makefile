#
# Makefile for the ttysnoop programs
#
CROSS_COMPILE=/home/user/extra/fsl-community-bsp/build/tmp/sysroots/i686-linux/usr/bin/armv5te-poky-linux-gnueabi/arm-poky-linux-gnueabi-

CC	= ${CROSS_COMPILE}gcc

# Without shadow support

CCOPTS	= -O2
#-lcrypt # remove -lcrypt if your system doesn't have it

# For shadow support

#CCOPTS	= -O2 -DSHADOW_PWD
#LIBS	= -lcrypt
#LIBS	= -lshadow

SERVEROBJS	= ttysnoops.o common.o
CLIENTOBJS	= ttysnoop.o common.o
SERVERSRCS	= ttysnoops.c
CLIENTSRCS	= ttysnoop.c
INCLUDES	= config.h common.h

all:		ttysnoops ttysnoop

ttysnoops:	$(SERVEROBJS)
		$(CC) $(SERVEROBJS) -o ttysnoops $(LIBS)

ttysnoop:	$(CLIENTOBJS)
		$(CC) $(CLIENTOBJS) -o ttysnoop $(LIBS)

ttysnoops.o:	$(SERVERSRCS) $(INCLUDES)
		$(CC) $(CCOPTS) -c -o ttysnoops.o $(SERVERSRCS)

ttysnoop.o:	$(CLIENTSRCS) $(INCLUDES)
		$(CC) $(CCOPTS) -c -o ttysnoop.o $(CLIENTSRCS)

common.o:	common.c common.h
		$(CC) $(CCOPTS) -c -o common.o common.c

clean:
		rm -f *.o core ttysnoop ttysnoops

install:
		install -s ttysnoop /sbin
		install -s ttysnoops /sbin
		install -m 644 ttysnoop.8 /usr/man/man8/
		@echo ... copy snooptab.dist to /etc/snooptab and edit it ...
 
