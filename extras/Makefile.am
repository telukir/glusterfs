addonexecdir = $(GLUSTERFS_LIBEXECDIR)
addonexec_SCRIPTS =
if WITH_SERVER
addonexec_SCRIPTS += peer_add_secret_pub
if USE_SYSTEMD
addonexec_SCRIPTS += mount-shared-storage.sh
endif
endif

EditorModedir = $(docdir)
EditorMode_DATA = glusterfs-mode.el glusterfs.vim

SUBDIRS = init.d systemd benchmarking hook-scripts $(OCF_SUBDIR) LinuxRPM \
          $(GEOREP_EXTRAS_SUBDIR) snap_scheduler firewalld cliutils python \
		  ganesha

confdir = $(sysconfdir)/glusterfs
if WITH_SERVER
conf_DATA = glusterfs-logrotate gluster-rsyslog-7.2.conf gluster-rsyslog-5.8.conf \
	    logger.conf.example glusterfs-georep-logrotate group-virt.example \
	    group-metadata-cache group-gluster-block group-nl-cache \
	    group-db-workload group-distributed-virt group-samba
endif

voldir = $(sysconfdir)/glusterfs
vol_DATA = thin-arbiter/thin-arbiter.vol
if WITH_SERVER
vol_DATA += glusterd.vol
endif

scriptsdir = $(datadir)/glusterfs/scripts
scripts_SCRIPTS = thin-arbiter/setup-thin-arbiter.sh
if WITH_SERVER
scripts_SCRIPTS += post-upgrade-script-for-quota.sh \
	pre-upgrade-script-for-quota.sh stop-all-gluster-processes.sh
if USE_SYSTEMD
scripts_SCRIPTS += control-cpu-load.sh
scripts_SCRIPTS += control-mem.sh
endif
endif

EXTRA_DIST = glusterfs-logrotate gluster-rsyslog-7.2.conf gluster-rsyslog-5.8.conf \
	logger.conf.example glusterfs-georep-logrotate group-virt.example \
	group-metadata-cache group-gluster-block group-nl-cache \
	group-db-workload group-samba specgen.scm glusterfs-mode.el glusterfs.vim \
	migrate-unify-to-distribute.sh backend-xattr-sanitize.sh \
	backend-cleanup.sh disk_usage_sync.sh clear_xattrs.sh \
	glusterd-sysconfig glusterd.vol post-upgrade-script-for-quota.sh \
	pre-upgrade-script-for-quota.sh command-completion/gluster.bash \
	command-completion/Makefile command-completion/README \
	stop-all-gluster-processes.sh clang-checker.sh mount-shared-storage.sh \
	control-cpu-load.sh control-mem.sh group-distributed-virt \
	thin-arbiter/thin-arbiter.vol thin-arbiter/setup-thin-arbiter.sh

install-data-local:
	if [ -n "$(tmpfilesdir)" ]; then \
		$(mkdir_p) $(DESTDIR)$(tmpfilesdir); \
		$(INSTALL_DATA) run-gluster.tmpfiles \
			$(DESTDIR)$(tmpfilesdir)/gluster.conf; \
	fi
if WITH_SERVER
	$(mkdir_p) $(DESTDIR)$(GLUSTERD_WORKDIR)/groups
	$(INSTALL_DATA) $(top_srcdir)/extras/group-virt.example \
		$(DESTDIR)$(GLUSTERD_WORKDIR)/groups/virt
	$(INSTALL_DATA) $(top_srcdir)/extras/group-metadata-cache \
		$(DESTDIR)$(GLUSTERD_WORKDIR)/groups/metadata-cache
	$(INSTALL_DATA) $(top_srcdir)/extras/group-gluster-block \
		$(DESTDIR)$(GLUSTERD_WORKDIR)/groups/gluster-block
	$(INSTALL_DATA) $(top_srcdir)/extras/group-nl-cache \
		$(DESTDIR)$(GLUSTERD_WORKDIR)/groups/nl-cache
	$(INSTALL_DATA) $(top_srcdir)/extras/group-db-workload \
		$(DESTDIR)$(GLUSTERD_WORKDIR)/groups/db-workload
	$(INSTALL_DATA) $(top_srcdir)/extras/group-distributed-virt \
		$(DESTDIR)$(GLUSTERD_WORKDIR)/groups/distributed-virt
	$(INSTALL_DATA) $(top_srcdir)/extras/group-samba \
		$(DESTDIR)$(GLUSTERD_WORKDIR)/groups/samba
endif
