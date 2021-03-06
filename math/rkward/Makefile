# Created by: thierry@pompo.net
# $FreeBSD$

PORTNAME=	rkward
DISTVERSION=	0.4.9a
PORTREVISION=	20
PORTEPOCH=	3
CATEGORIES=	math
MASTER_SITES=	SF/${PORTNAME}/Historical_Releases/0.4.x_and_earlier/0.4.9a%20%28KDE3%29

MAINTAINER=	thierry@FreeBSD.org
COMMENT=	IDE/GUI for the R-project

BUILD_DEPENDS=	${LOCALBASE}/bin/R:${PORTSDIR}/math/R
RUN_DEPENDS=	${LOCALBASE}/bin/R:${PORTSDIR}/math/R

CONFLICTS=	rkward-kde4-0.5.*

USE_KDELIBS_VER=3
USE_PHP=	yes
WANT_PHP_CLI=	yes
USES=		gettext
USE_AUTOTOOLS=	libtool
CONFIGURE_ENV=	PTHREAD_CFLAGS="${PTHREAD_CFLAGS}"	\
		PTHREAD_LIBS="${PTHREAD_LIBS}"
CONFIGURE_ARGS=	--disable-fast-perl

USE_FORTRAN=	yes
FORTRANLIBDIR2=	`${DIRNAME} \\`${FC} -print-libgcc-file-name\\``/../../../

DOCSDIR=	${PREFIX}/share/doc/HTML/en/rkward

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MNLS}
NLS=		""
.else
NLS=		"@comment "
.endif
PLIST_SUB+=	NLS=${NLS}

PHP2FIX=	rkward/plugins/makemakefileam.php	\
		rkward/settings/rksettingsmodulephp.cpp

pre-configure:
	${REINPLACE_CMD} -e 's|/usr/bin/php|${LOCALBASE}/bin/php|'	\
		${PHP2FIX:S|^|${WRKSRC}/|}
	${REINPLACE_CMD} -e 's|-lgfortran|-L${FORTRANLIBDIR2} -lgfortran|'	\
		${WRKSRC}/${CONFIGURE_SCRIPT}
.if ! ${PORT_OPTIONS:MDOCS}
	${REINPLACE_CMD} -e 's|rkward po doc|rkward po|'	\
		${WRKSRC}/Makefile.in
.endif
.if ! ${PORT_OPTIONS:MNLS}
	${REINPLACE_CMD} -e 's|SUBDIRS = rkward po|SUBDIRS = rkward|'	\
		${WRKSRC}/Makefile.in
.endif
	@(if [ ! -e ${LOCALBASE}/lib/R/lib/libR.so ] ; then \
	${ECHO_MSG} "==> ${PKGNAME} requires math/R to be built WITH_LIBR" ; \
	exit 1; fi)

.include <bsd.port.mk>
