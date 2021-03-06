# Created by: desmo@bandwidth.org
# $FreeBSD$

PORTNAME=	LPRng
PORTVERSION=	3.8.35
PORTREVISION=	1
CATEGORIES=	sysutils print
MASTER_SITES=	ftp://ftp.lprng.com/pub/%SUBDIR%/ \
		ftp://ftp.cise.ufl.edu/pub/mirrors/%SUBDIR%/ \
		ftp://ftp.cs.umn.edu/pub/%SUBDIR%/ \
		ftp://ftp.informatik.uni-hamburg.de/pub/os/unix/utils/%SUBDIR%/ \
		ftp://ftp.uni-paderborn.de/pub/unix/printer/%SUBDIR%/
MASTER_SITE_SUBDIR=	LPRng/LPRng
EXTRACT_SUFX=	.tgz

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Enhanced Printer Spooler

LIB_DEPENDS=	gdbm:${PORTSDIR}/databases/gdbm

CONFLICTS=	cups-base-1.[2-9]*

GNU_CONFIGURE=	yes
USE_LDCONFIG=	yes

USE_RC_SUBR=	${PORTNAME:L}

SUB_FILES=	pkg-message pkg-install
SUB_LIST=	SYSCONFDIR="${SYSCONFDIR}"

PKGDEINSTALL=	${PKGINSTALL}

CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib
CONFIGURE_ARGS=	\
		--with-sbindir=${PREFIX}/sbin \
		--with-filterdir=${PREFIX}/libexec/filters \
		--with-filter_path="${PREFIX}/bin:/bin:/usr/bin:${PREFIX}/sbin:/sbin:/usr/sbin" \
		--with-lpd_conf_path=${SYSCONFDIR}/lpd.conf \
		--with-lpd_perms_path=${SYSCONFDIR}/lpd.perms \
		--with-printcap_path=/etc/printcap \
		--with-ld_library_path="${PREFIX}/lib:/lib:/usr/lib:/${LOCALBASE}/lib" \
		--enable-gdbm=${LOCALBASE} \
		--disable-werror

.if defined(PORT_REPLACES_BASE_LPR)
PREFIX=		/usr
SYSCONFDIR=	/etc
.endif

.if defined(SYSCONFDIR)
CONFIGURE_ARGS+=	--sysconfdir="${SYSCONFDIR}"
PLIST_SUB+=	CWD="" SYSCONFDIR="${SYSCONFDIR:S,^/,,}"
.else
SYSCONFDIR=	${PREFIX}/etc
PLIST_SUB+=	CWD="@comment " SYSCONFDIR="${SYSCONFDIR:S,^${PREFIX}/,,}"
.endif

MAN1=	lpf.1 psbanner.1 lp.1 cancel.1 lprng_certs.1 lprng_index_certs.1 \
	lpstat.1 lpq.1 lpr.1 lprm.1 monitor.1 pclbanner.1 lpbanner.1
MAN5=	printcap.5 lpd.conf.5 lpd.perms.5
MAN8=	lpc.8 checkpc.8 lpd.8

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MNLS}
USES+=			gettext
PLIST_SUB+=		NLS=""
.else
CONFIGURE_ARGS+=	--disable-nls
PLIST_SUB+=		NLS="@comment "
.endif

pre-everything::
	@${ECHO_MSG} "If you want to replace the default printing system with LPRng, use:"
	@${ECHO_MSG} "  make PORT_REPLACES_BASE_LPR=yes clean all install"
	@${ECHO_MSG} " OR"
	@${ECHO_MSG} "  make CONFIGURE_SCRIPT=STANDARD_configuration clean all install"
	@if [ "${PREFIX}" = "/usr" -a ! -d /usr/man ] ; then \
		${ECHO_MSG} "The man pages will be installed in /usr/man." ; \
		${ECHO_MSG} "You should make a symbolic link /usr/share/man from /usr/man"; \
		${ECHO_MSG} "   ln -s /usr/share/man /usr/man"; \
		${ECHO_MSG} "If you do not, you will retain the old FreeBSD man pages."; \
		${ECHO_MSG} "See the hier(7) man page for details of the FreeBSD file system"; \
		${ECHO_MSG} "layout.  Configure is not equipped to determine the location of"; \
		${ECHO_MSG} 'man pages and defaults to $${PREFIX}/man, which is incorrect for FreeBSD.'; \
	fi

post-patch:
	@${ECHO} "#! /bin/sh" > ${WRKSRC}/postinstall.freebsd.sh
	@${REINPLACE_CMD} -e 's,$${INSTALL} $$$$i $${DATADIR}/$$$$i.sample,true &,' \
		${WRKSRC}/Makefile.in

pre-install: apply-slist
	@${SH} ${PKGINSTALL} ${PKGNAME} PRE-INSTALL

post-install:
	@${INSTALL_DATA} ${WRKSRC}/lpd.conf ${SYSCONFDIR}/lpd.conf.sample
	@${INSTALL_DATA} ${WRKSRC}/lpd.perms ${SYSCONFDIR}/lpd.perms.sample
	@${INSTALL_DATA} ${WRKSRC}/printcap ${SYSCONFDIR}/printcap.sample
.if ${PORT_OPTIONS:MDOCS}
	@${INSTALL} -d -o ${SHAREOWN} -g ${SHAREGRP} -m 0555 ${DOCSDIR}
	@${INSTALL} -d -o ${SHAREOWN} -g ${SHAREGRP} -m 0555 ${DOCSDIR}/Reference
	@${INSTALL} -d -o ${SHAREOWN} -g ${SHAREGRP} -m 0555 ${DOCSDIR}/PrintingCookbook
.for ext in html pdf ppt ps txt gif jpg png
	@for i in `${LS} ${WRKSRC}/DOCS | ${GREP} "\.${ext}$$"`; \
		do ${INSTALL_DATA} ${WRKSRC}/DOCS/$$i ${DOCSDIR}; done
	@for i in `${LS} ${WRKSRC}/PrintingCookbook/HTML | ${GREP} "\.${ext}$$"`; \
		do ${INSTALL_DATA} ${WRKSRC}/PrintingCookbook/HTML/$$i ${DOCSDIR}/PrintingCookbook; done;
.endfor
.endif
	@${SH} ${PKGINSTALL} ${PKGNAME} POST-INSTALL
	@${CAT} ${PKGMESSAGE}

.include <bsd.port.mk>
