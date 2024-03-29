
################################################################################
## set flags for golobal compile and link setting.
################################################################################

CONFIG_FOR_COMPILE = $(CFLAGS) $(LOCAL_CFLAGS)
CONFIG_FOR_LINK = -Wl,--no-undefined


################################################################################

BuildPath      = ./build
ObjectPath     = $(BuildPath)/obj
OutputPath     = ./
DependFilePath = $(BuildPath)/dep
Target         = $(OutputPath)/libtplayer.so   ## output target.

ifneq ($(BuildPath),wildcard($(BuildPath)))
a := $(shell mkdir -p $(BuildPath))
endif
ifneq ($(ObjectPath),wildcard($(ObjectPath)))
a := $(shell mkdir -p $(ObjectPath))
endif
ifneq ($(OutputPath),wildcard($(OutputPath)))
a := $(shell mkdir -p $(OutputPath))
endif
ifneq ($(DependFilePath),wildcard($(DependFilePath)))
a := $(shell mkdir -p $(DependFilePath))
endif


################################################################################
## set the source files, object files and dependency files
################################################################################
## set the source path to VPATH.
SourcePath = $(shell find ./ -type d)
SourcePath := $(filter-out $(BuildPath) $(ObjectPath) $(DependFilePath), $(SourcePath))
VPATH := $(SourcePath)

## set the source files.
SourceFiles  = $(foreach dir,$(SourcePath),$(shell find $(dir) -maxdepth 1 -name "*.c"))

## set the object files.
ObjectFiles = $(addprefix $(ObjectPath)/, $(addsuffix .o ,$(basename $(notdir $(SourceFiles)))))

## set the dependency files.
DependFiles = $(addprefix $(DependFilePath)/, $(addsuffix .d ,$(notdir $(basename $(SourceFiles)))))


################################################################################
## set flags for compile and link
################################################################################

## set the include path for compile flags.
SourceIncludePath = $(foreach dir,$(SourcePath),-I$(dir)) \
				-I ../ \
				-I../libcedarc/include \
			        -I../libcedarc/vdecoder/include \
			        -I../libcedarx/ \
			        -I../libcedarx/external/include/adecoder \
			        -I../libcedarx/external/include/sdecoder \
			        -I../libcedarx/libcore/playback/include \
			        -I../libcedarx/libcore/common/iniparser\
			        -I../libcedarx/libcore/parser/include/ \
			        -I../libcedarx/libcore/stream/include/ \
			        -I../libcedarx/libcore/base/include/ \
			        -I../libcedarx/xplayer/include
## set compile flags
CompileFlags = $(CONFIG_FOR_COMPILE) $(SourceIncludePath) -Wall -O2 -ldl

##set link flag path
ifeq ($(BOARD_PLATFORM),$(filter $(BOARD_PLATFORM),r18 r30))
    ifeq ($(C_LIB_TYPE),musl)
        ifeq ($(KERNEL64_USER32),y)
            LocalAudioGain += ./arm-musl/libAudioGain.a
        else
            LocalAudioGain += ./aarch64-musl/libAudioGain.a
        endif
    endif
    ifeq ($(C_LIB_TYPE),glibc)
        ifeq ($(KERNEL64_USER32),y)
            LocalAudioGain += ./arm-glibc/libAudioGain.a
        else
            LocalAudioGain += ./aarch64-glibc/libAudioGain.a
        endif
    endif
endif

ifeq ($(BOARD_PLATFORM),$(filter $(BOARD_PLATFORM),r16 r58 r40 r311 r11 r7 v306 r333 r331 r7s g102 t7 r332 mr133 r328s2 r328s3))
    ifeq ($(C_LIB_TYPE),musl)
        LocalAudioGain += ./arm-musl/libAudioGain.a
    endif
    ifeq ($(C_LIB_TYPE),glibc)
        LocalAudioGain += ./arm-glibc/libAudioGain.a
    endif
endif

ifeq ($(BOARD_PLATFORM),$(filter $(BOARD_PLATFORM),r6 c200s))
    ifeq ($(C_LIB_TYPE),musl)
        LocalAudioGain += ./arm9-musl/libAudioGain.a
    endif
    ifeq ($(C_LIB_TYPE),glibc)
        LocalAudioGain += ./arm9-glibc/libAudioGain.a
    endif
endif

################################################################################
## make commands, all/clean/cleanall
################################################################################

## define commands for make, sush as all, clean
.PHONY: all clean cleantarget cleanall
all:$(Target)

clean:
	-rm -f $(ObjectPath)/*
	-rm -f $(Target)

cleanall: clean
	-rm -f $(DependFilePath)/*
	-rm -rf $(BuildPath)


################################################################################
## define target dependencies.
################################################################################

## compile source files to object files.
#$(ObjectPath)/%.o:%.c
#	$(CC) $(CompileFlags) -o $@ -c $< -fPIC -shared
$(ObjectFiles):$(ObjectPath)/%.o:%.c
	@echo =======$(CONFIG_FOR_COMPILE)===
	@echo =======CPP:$(CPP)====
	@echo =======CXX:$(CXX)====
	$(CC) $(CompileFlags) -o $@ -c $< -fPIC -shared

## link object files to the target share library.
$(Target):$(ObjectFiles)
	@echo ===llhplatform====$(BOARD_PLATFORM)===
	@echo ===llhaudio====$(LocalAudioGain)===
	@echo ===llhlibtype====$(C_LIB_TYPE)===
	$(CC) -o $@ $^ -fPIC -shared $(LDFLAGS) $(LocalAudioGain)

## set rules to generate .d files.
$(DependFilePath)/%.d:%.c
	set -e; rm -f $@; \
	$(CC) -MM $(CompileFlags) $< > $@.$$$$; \
	sed 's,\($*\)\.o[:]*,$(ObjectPath)/\1.o $@: ,g' < $@.$$$$ > $@; \
	rm -f $@.$$$$

## include the .d files to set dependency rules.
ifneq ($(MAKECMDGOALS),clean)
ifneq ($(MAKECMDGOALS),cleantarget)
ifneq ($(MAKECMDGOALS),cleanall)
-include $(DependFiles)
endif
endif
endif
