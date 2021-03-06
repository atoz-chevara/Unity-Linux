
include Rules.mk

PODIRS = $(MKLIVECDPODIR) $(MKREMASTERPODIR)
SUBDIRS = $(MKREMASTERDIR) $(PODIRS)

all:
	@for d in $(SUBDIRS); do ( cd $$d ; make ) ; done
	@$(MKDIR) -p $(DISTDIR)
	@$(CAT) $(SRCDIR)/hwdetect2.in | \
		$(SED) -e 's,@MKLIVECDVER@,$(ARCHIVEVER),g' | \
		$(SED) -e 's,@DEF_KEYBOARD@,$(DEF_KEYBOARD),g' | \
		$(SED) -e 's,@MAX_SPLASH@,$(MAX_SPLASH),g' | \
		$(SED) -e 's,@VAL_SPLASH_FULL@,$(VAL_SPLASH_FULL),g' | \
		$(SED) -e 's,@VAL_SPLASH_LINUXRC@,$(VAL_SPLASH_LINUXRC),g' | \
		$(SED) -e 's,@VAL_SPLASH_SYSINIT@,$(VAL_SPLASH_SYSINIT),g' | \
		$(SED) -e 's,@VAL_SPLASH_HWDETECT@,$(VAL_SPLASH_HWDETECT),g' \
			>$(DISTDIR)/hwdetect2
	@$(CAT) $(SRCDIR)/linuxrc.in | \
		$(SED) -e 's,@MKLIVECDVER@,$(ARCHIVEVER),g' | \
		$(SED) -e 's,@KERNELVER@,$(KERNELVER),g' | \
		$(SED) -e 's,@MAX_SPLASH@,$(MAX_SPLASH),g' | \
		$(SED) -e 's,@VAL_SPLASH_FULL@,$(VAL_SPLASH_FULL),g' | \
		$(SED) -e 's,@VAL_SPLASH_LINUXRC@,$(VAL_SPLASH_LINUXRC),g' | \
		$(SED) -e 's,@VAL_SPLASH_SYSINIT@,$(VAL_SPLASH_SYSINIT),g' | \
		$(SED) -e 's,@VAL_SPLASH_HWDETECT@,$(VAL_SPLASH_HWDETECT),g' \
			>$(DISTDIR)/linuxrc
	@$(CP) $(SRCDIR)/halt.local.in $(DISTDIR)/halt.local
	@$(CP) $(MKREMASTERDIR)/mkremaster.in $(DISTDIR)/mkremaster
	@$(CP) $(MKREMASTERDIR)/*.desktop $(DISTDIR)/
	@$(CP) $(MKREMASTERDIR)/mkremaster.png $(DISTDIR)/
	@$(CP) $(SRCDIR)/gfxboot.cfg.in $(DISTDIR)/gfxboot.cfg
	@$(CP) $(SRCDIR)/finish-install.in $(DISTDIR)/finish-install
	@$(CP) $(SRCDIR)/fstab.in $(DISTDIR)/fstab
	@$(CAT) $(SRCDIR)/rc.sysinit.in | \
		$(SED) -e 's,@MAX_SPLASH@,$(MAX_SPLASH),g' | \
		$(SED) -e 's,@VAL_SPLASH_FULL@,$(VAL_SPLASH_FULL),g' | \
		$(SED) -e 's,@VAL_SPLASH_LINUXRC@,$(VAL_SPLASH_LINUXRC),g' | \
		$(SED) -e 's,@VAL_SPLASH_SYSINIT@,$(VAL_SPLASH_SYSINIT),g' | \
		$(SED) -e 's,@VAL_SPLASH_HWDETECT@,$(VAL_SPLASH_HWDETECT),g' \
			>$(DISTDIR)/rc.sysinit
	@$(CAT) $(SRCDIR)/$(PKGNAME).in | \
		$(SED) -e 's,@PKGNAME@,$(PKGNAME),g' | \
		$(SED) -e 's,@MKLIVECDVER@,$(ARCHIVEVER),g' | \
		$(SED) -e 's,@DEF_KEYBOARD@,$(DEF_KEYBOARD),g' | \
		$(SED) -e 's,@DEF_UNION@,$(DEF_UNION),g' | \
		$(SED) -e 's,@DEF_RESOLUTION@,$(DEF_RESOLUTION),g' | \
		$(SED) -e 's,@DEF_VGAMODE@,$(DEF_VGAMODE),g' \
			>$(DISTDIR)/$(PKGNAME)

install:
	@echo
	@echo '                     ***Installation START***'
	@echo
	@$(MKDIR) -p $(DESTDIR)$(SHAREDIR)
	@echo 'Created directory $(DESTDIR)$(SHAREDIR)'
	@$(MKDIR) -p $(DESTDIR)$(SBINDIR)
	@echo 'Created directory $(DESTDIR)$(SBINDIR)'
	@$(MKDIR) -p $(DESTDIR)$(DESKTOPDIR)
	@echo 'Created directory $(DESTDIR)$(DESKTOPDIR)'
	@$(MKDIR) -p $(DESTDIR)$(ICONSDIR)
	@echo 'Created directory $(DESTDIR)$(ICONSDIR)'
	@$(INSTALL) -m 644 $(DISTDIR)/linuxrc $(DESTDIR)$(SHAREDIR)
	@echo 'Installed linuxrc to $(DESTDIR)$(SHAREDIR)'
	@$(INSTALL) -m 644 $(DISTDIR)/halt.local $(DESTDIR)$(SHAREDIR)
	@echo 'Installed halt.local to $(DESTDIR)$(SHAREDIR)'
	@$(INSTALL) -m 644 $(DISTDIR)/rc.sysinit $(DESTDIR)$(SHAREDIR)
	@echo 'Installed rc.sysinit to $(DESTDIR)$(SHAREDIR)'
	@$(INSTALL) -m 644 $(DISTDIR)/*.desktop $(DESTDIR)$(DESKTOPDIR)
	@echo 'Installed desktop files to $(DESTDIR)$(DESKTOPDIR)'
	@$(INSTALL) -m 755 $(DISTDIR)/$(PKGNAME) $(DESTDIR)$(SBINDIR)
	@echo 'Installed $(PKGNAME) to $(DESTDIR)$(SBINDIR)'
	@$(INSTALL) -m 755 $(DISTDIR)/hwdetect2 $(DESTDIR)$(SBINDIR)
	@echo 'Installed hwdetect2 to $(DESTDIR)$(SBINDIR)'
	@$(INSTALL) -m 755 $(DISTDIR)/mkremaster $(DESTDIR)$(SBINDIR)
	@echo 'Installed mkremaster to $(DESTDIR)$(SBINDIR)'
	@$(INSTALL) -m 644 $(DISTDIR)/mkremaster.png $(DESTDIR)$(ICONSDIR)
	@echo 'Installed mkremaster.png to $(DESTDIR)$(ICONSDIR)'
	@$(INSTALL) -m 644 $(DISTDIR)/gfxboot.cfg $(DESTDIR)$(SHAREDIR)
	@echo 'Installed gfxboot.cfg to $(DESTDIR)$(SHAREDIR)'
	@$(INSTALL) -m 755 $(DISTDIR)/finish-install $(DESTDIR)$(SHAREDIR)
	@echo 'Installed finish-install to $(DESTDIR)$(SHAREDIR)'
	@$(INSTALL) -m 644 $(DISTDIR)/fstab $(DESTDIR)$(SHAREDIR)
	@echo 'Installed fstab to $(DESTDIR)$(SHAREDIR)'
	@for d in $(SUBDIRS); do ( cd $$d ; make $@ ) ; done
	@echo
	@echo '                     ***Installation END***'
	@echo

install-doc:
	$(MKDIR) -p $(DESTDIR)$(DOCDIR)
	$(CP) -f $(DOCDIST) $(DOCDIR)

$(PKGNAME).spec: $(PKGNAME).spec.in
	@$(MKDIR) -p $(DISTDIR)
	@$(CAT) $(PKGNAME).spec.in | \
		$(SED) -e 's,@MKLIVECDVER@,$(MKLIVECDVER),g' | \
		$(SED) -e 's,@MKLIVECDREL@,$(MKLIVECDREL),g'  \
			>$(PKGNAME).spec
	@echo
	@echo "$(PKGNAME).spec generated in $$PWD"
	@echo

spec: $(PKGNAME).spec

spec-update: spec
ifeq ($(SPLOG),)
	$(error Can't find splog. Please, install 'pkgutils' and retry)
endif

ifeq ($(pname),)
	$(error Please, define the packager name by appending 'pname=name_of_the_packager')
endif 

ifeq ($(pmail),)
	$(error Please, define the packager e-mail by appending 'pmail=e-mail_of_the_packager')
endif

ifeq ($(taglist),)
	$(error Please, define the tag list by appending 'taglist="-t \"sentence to log\" -t \"other sentence to log\""')
endif

	@$(SPLOG) -p "$(pname) <$(pmail)>" $(taglist) $(PKGNAME).spec
	@echo
	@echo "The %changelog section of $(PKGNAME).spec has been updated with the provided info."
	@echo "Run 'make spec-merge' if you want to merge it back into the spec template, but first check it out!"
	@echo

spec-merge: spec
	@head -n $$(($$(grep -n "%changelog" $(PKGNAME).spec.in | cut -f1 -d:)-1)) $(PKGNAME).spec.in > temp.spec
	@tail -n $$(($$(wc -l < $(PKGNAME).spec)-$$(grep -n "%changelog" $(PKGNAME).spec | cut -f1 -d:)+1)) $(PKGNAME).spec >> temp.spec
	@mv -f temp.spec $(PKGNAME).spec.in
	@echo
	@echo "The %changelog section of $(PKGNAME).spec has been merged back into the spec template."
	@echo

lang-update: clean
	@for d in $(PODIRS); do ( cd $$d ; $(RM) -f *.pot ) ; done
	@for d in $(PODIRS); do ( cd $$d ; make update_n_merge ) ; done
	@echo
	@echo "All lang files are now up to date"
	@echo

clean:
	@$(RM) -f *.spec
	@$(RM) -rf $(MKLIVECDDIST)
	@$(RM) -rf $(DISTDIR)
	@$(RM) -rf $(MKLIVECDDIST).tar.xz*
	@find -name '*~' -exec $(RM) {} \;
	@for d in $(SUBDIRS); do ( cd $$d ; make $@ ) ; done
	@echo
	@echo "Cleaning complete"
	@echo

dist: all spec
	@$(MKDIR) -p $(MKLIVECDDIST)/$(SRCDIR)
	@$(MKDIR) -p $(MKLIVECDDIST)/$(MKLIVECDPODIR)
	@$(MKDIR) -p $(MKLIVECDDIST)/$(MKREMASTERPODIR)
	@$(CP) $(DOCDIST) $(MKLIVECDDIST)
	@$(CP) $(BUILDDIST) $(MKLIVECDDIST)
	@$(CP) $(SRCDIST) $(MKLIVECDDIST)/$(SRCDIR)
	@$(CP) $(MKLIVECDPODIST) $(MKLIVECDDIST)/$(MKLIVECDPODIR)
	@$(CP) $(MKREMASTERDIST) $(MKLIVECDDIST)/$(MKREMASTERDIR)
	@$(CP) $(MKREMASTERPODIST) $(MKLIVECDDIST)/$(MKREMASTERPODIR)

tar: dist
	@$(TAR) -Jcvf $(MKLIVECDDIST).tar.xz $(MKLIVECDDIST)
	@$(MD5SUM) $(MKLIVECDDIST).tar.xz \
		>$(MKLIVECDDIST).tar.xz.md5
	@$(RM) -rf $(MKLIVECDDIST)
	@echo
	@echo "$(MKLIVECDDIST).tar.xz and $(MKLIVECDDIST).tar.xz.md5 generated in $$PWD"
	@echo

rpm: tar
	$(RPMBUILD) -ta $(MKLIVECDDIST).tar.xz --clean

version:
	@echo
	@echo "$(PKGNAME), $(MKLIVECDVER)-$(MKLIVECDREL)"
	@echo

maintenance-help:
	@echo
	@echo '                  ********************************'
	@echo '                  ******MKLIVECD MAINTENANCE******'
	@echo '                  ********************************'
	@echo
	@echo '* SPEC UPDATE'
	@echo
	@echo ' Make sure you have bumped the release, or updated the version by'
	@echo ' modifying the values of MAJORVER, MINORVER, PATCHVER, RELVER in'
	@echo ' Rules.mk.'
	@echo ' Bear in mind that VERSION=MAJORVER.MINORVER.PATCHVER, whereas'
	@echo ' RELEASE=RELVER'
	@echo
	@echo ' [Please, note that you can view what the current version and'
	@echo ' release are by running `make version`]'
	@echo 
	@echo ' Once you have done that, and once you are happy with all your'
	@echo ' modifications, update the spec file with the following command:'
	@echo 
	@echo ' make spec-update pname="PKGRNAME" pmail="PKGRMAIL" taglist="TAGS"'
	@echo 
	@echo ' Where:'
	@echo '         PKGRNAME is the name of the packager'
	@echo 
	@echo '         PKGRMAIL is the e-mail address of the packager'
	@echo 
	@echo '         TAGS is a list of sentences to be logged in the Changelog'
	@echo '         in the form'
	@echo '         "-t \"First sentence to log\" -t \"Second sentence to log\""'
	@echo
	@echo ' Example:'
	@echo '          make spec-update pname="Unity packager" \'
	@echo '          pmail="packager@unity-linux.org" taglist="-t \"New version\""'
	@echo
	@echo ' If you are happy with the spec, you must merge back the updated'
	@echo ' Changelog into the spec template $(PKGNAME).spec.in'
	@echo ' In order to do so, use the following command:'
	@echo
	@echo ' make spec-merge'
	@echo
	@echo ' Please, note that you must edit $(PKGNAME).spec.in directly, if you'
	@echo ' need to modify any section of the spec other than the Changelog.'
	@echo
	@echo
	@echo '* TARBALL CREATION'
	@echo
	@echo ' You can easily create a tarball with the updated files with the'
	@echo ' following command:'
	@echo
	@echo ' make tar'
	@echo
	@echo
	@echo '* LANGUAGE FILES UPDATE'
	@echo
	@echo ' To update the template catalog and merge all language files with'
	@echo ' the new template, use the following command:'
	@echo
	@echo ' make lang-update'
	@echo
	@echo
	@echo '* TESTING INSTALL'
	@echo
	@echo ' If you want to check whether the install procedure runs smoothly, you'
	@echo ' might want to install to a different destination (for example: your'
	@echo ' home directory).'
	@echo ' Set the DESTDIR variable (case-sensitive) in this way:'
	@echo
	@echo ' make DESTDIR=/path/to/destination/dir install'
	@echo
	@echo 
	@echo 'NOTE: Whenever you change something, and you want to rebuild the spec,'
	@echo '      the tarball, etc., and especially before committing your changes,'
	@echo '      always launch first:'
	@echo
	@echo '      make clean'
	@echo
	@echo 
