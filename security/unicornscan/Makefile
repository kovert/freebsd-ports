# New ports collection makefile for:	unicornscan
# Date created:		4 October 2004
# Whom:			cykyc
#
# $FreeBSD$
#

PORTNAME=	unicornscan
PORTVERSION=	0.4.2
PORTREVISION=	4
CATEGORIES=	security
MASTER_SITES=	http://www.unicornscan.org/releases/

MAINTAINER=	cykyc@yahoo.com
COMMENT=	Next-generation of udpscan plus a high-speed TCP scanner

LIB_DEPENDS=	net:${PORTSDIR}/net/libnet

USE_GMAKE=	yes
MAKE_ENV=	LIBNET_CONFIG="${LIBNET_CONFIG}"
CFLAGS+=	-DWITH_LONGOPTS

MAN1=		unicornscan.1

PKGMESSAGE=	${WRKDIR}/pkg-message

LIBNET_CONFIG?=	${LOCALBASE}/bin/libnet11-config

.include <bsd.port.pre.mk>

post-patch:
.for text in pkg-message
	@${SED} -e 's,%%PREFIX%%,${PREFIX},g' \
	${PKGDIR}/${text} >${WRKDIR}/${text}
.endfor
	@${REINPLACE_CMD} -e 's|-lnet|`${LIBNET_CONFIG} --libs`|' \
		${WRKSRC}/src/scan_progs/Makefile ${WRKSRC}/src/tools/Makefile

do-install:
	${MKDIR} ${PREFIX}/etc/unicornscan
	${MKDIR} ${PREFIX}/libexec/unicornscan/modules
	${MKDIR} ${PREFIX}/share/unicornscan
	${MKDIR} ${PREFIX}/var/unicornscan
	${INSTALL_PROGRAM} ${WRKSRC}/src/unicornscan ${PREFIX}/bin/
	${INSTALL_PROGRAM} ${WRKSRC}/src/tools/fantaip ${PREFIX}/bin/
	${INSTALL_PROGRAM} ${WRKSRC}/src/scan_progs/unisend ${PREFIX}/libexec/unicornscan
	${INSTALL_PROGRAM} ${WRKSRC}/src/scan_progs/unilisten ${PREFIX}/libexec/unicornscan
	${REINPLACE_CMD} -e 's|/usr/local/share|${PREFIX}/etc|' \
		${WRKSRC}/fconf/unicorn.conf
	for confs in ${WRKSRC}/fconf/*.conf; do\
		${INSTALL_DATA} $$confs ${PREFIX}/etc/unicornscan/`basename $$confs`.sample ;\
	done
	${INSTALL_DATA} ${WRKSRC}/fconf/port-numbers ${PREFIX}/share/unicornscan
	for mods in ${WRKSRC}/src/payload_modules/*.so; do\
		${INSTALL_PROGRAM} $$mods ${PREFIX}/libexec/unicornscan/modules/ ;\
	done
	for mods in ${WRKSRC}/src/report_modules/shlibs/*.so; do\
		${INSTALL_PROGRAM} $$mods ${PREFIX}/libexec/unicornscan/modules/ ;\
	done
	for pofs in p0f.fp p0fa.fp p0fr.fp; do\
		${INSTALL_DATA} ${WRKSRC}/src/report_modules/p0f/$$pofs ${PREFIX}/share/unicornscan/ ;\
	done
	${INSTALL_PROGRAM} ${WRKSRC}/src/report_modules/shlibs/libp0f.so \
		${PREFIX}/libexec/unicornscan/modules/
	${INSTALL_MAN} ${WRKSRC}/docs/unicornscan.1 ${PREFIX}/man/man1/
	for files in LICENSE README misc/UDP_PAYLOADS_NEEDED \
	TODO_BUGSTOFIX README.database; do\
		${INSTALL_DATA} ${WRKSRC}/$$files ${PREFIX}/share/unicornscan/ ;\
	done
	@${CAT} ${PKGMESSAGE}

.include <bsd.port.post.mk>
