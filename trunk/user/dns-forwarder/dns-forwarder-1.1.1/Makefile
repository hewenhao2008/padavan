# Makefile for dns-forwarder
 
PP=$(CONFIG_CROSS_COMPILER_PATH)/mipsel-linux-uclibc-cpp -mips32r2 -march=mips32r2
CC=$(CONFIG_CROSS_COMPILER_PATH)/mipsel-linux-uclibc-gcc -mips32r2 -march=mips32r2
CCFLAGS=-O3 -pipe -ffast-math -ftree-vectorize -Werror -Wall
LDFLAGS=
 
SRCDIR=src
BINDIR=src
BUILDDIR=src
 
TARGET=$(BINDIR)/dns-forwarder
CCOBJSFILE=$(BUILDDIR)/ccobjs
-include $(CCOBJSFILE)
LDOBJS=$(patsubst $(SRCDIR)%.c,$(BUILDDIR)%.o,$(CCOBJS))
 
DEPEND=$(LDOBJS:.o=.dep)
 
all : $(CCOBJSFILE) $(TARGET)
	@$(RM) $(CCOBJSFILE)
 
clean : 
	@echo -n "Clean ... " && $(RM) $(TARGET) $(CCOBJSFILE) $(BUILDDIR)/*.dep  $(BUILDDIR)/*.o && echo "OK"
 
$(CCOBJSFILE) : 
	@echo CCOBJS=`ls $(SRCDIR)/*.c` > $(CCOBJSFILE)
 
$(TARGET) : $(LDOBJS)
	@echo -n "Linking $^ to $@ ... " && $(CC) -o $@ $^ $(LDFLAGS) && echo "OK"
 
$(BUILDDIR)/%.dep : $(SRCDIR)/%.c
	@$(PP) $(CCFLAGS) -MM -MT $(@:.dep=.o) -o $@ $<
 
$(BUILDDIR)/%.o : $(SRCDIR)/%.c
	@echo -n "Building $< ... " && $(CC) $(CCFLAGS) -c -o $@ $< && echo "OK"
 
-include $(DEPEND)
