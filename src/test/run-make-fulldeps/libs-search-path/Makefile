-include ../tools.mk

ifdef IS_MSVC

TARGETS =
ifeq ($(filter x86,$(LLVM_COMPONENTS)),x86)
TARGETS += x86_64-windows-msvc
endif

all: $(TARGETS)

define MK_TARGETS
$(1): empty.rs
	mkdir $$(TMPDIR)/obj
	$$(call COMPILE_OBJ,$$(TMPDIR)/obj/crt2.o,crt2.c)
	$$(RUSTC) --target $(1) -L$$(TMPDIR)/obj -Z print-link-args empty.rs \
		| $$(CGREP) $$(TMPDIR)/obj/crt2.o
endef

$(foreach target,$(TARGETS),$(eval $(call MK_TARGETS,$(target))))

else

all:

endif
