# Created by: Alexey Dokuchaev <danfe@FreeBSD.org>
# $FreeBSD$

PORTNAME=	relay
PORTVERSION=	0.4
CATEGORIES=	games
MASTER_SITES=	${MASTER_SITE_LOCAL} http://freebsd.nsu.ru/distfiles/
MASTER_SITE_SUBDIR=	danfe
PKGNAMEPREFIX=	${Q2PKGNAMEPREFIX}
DISTNAME=	relay-${PORTVERSION}.src

MAINTAINER=	danfe@FreeBSD.org
COMMENT=	Quake II multi-view demo recording facility

LICENSE=	GPLv2

USE_GMAKE=	yes
MAKE_ARGS=	MODE=release OBJ_DIR=. OUT_DIR=. Q2MODULE=game.so \
		QUAKE2_DIR="${Q2DIR}" BIN_DIR="${PREFIX}/bin" \
		CC="${CC}" CFLAGS="${CFLAGS}"

WRKSRC=		${WRKDIR}/relay-${PORTVERSION}
PORTDOCS=	FAQ README

OPTIONS_DEFINE=	DOCS

.include "${.CURDIR}/../quake2-data/Makefile.include"
.include <bsd.port.options.mk>

.if ${ARCH} == "amd64" || ${ARCH} == "ia64"
CFLAGS+=	-fPIC
.endif

post-patch: .SILENT
	${REINPLACE_CMD} -e 's/-ldl// ; /^include/d ; \
		s/cp -p/${INSTALL_PROGRAM}/' ${WRKSRC}/Makefile
	${REINPLACE_CMD} -e '/random/d' ${WRKSRC}/replay/rp_local.h
	${REINPLACE_CMD} -e 's,<malloc\.h>,<stdlib\.h>,' \
		${WRKSRC}/common/mem.c
	cd ${WRKSRC}/common && ${SH} -c 'for i in *.h; do \
		${ECHO_CMD} >> $${i}; done'
# Reorganize #include's (use /bin/ed to avoid a patch)
	${ECHO_CMD} -e '35t30\n36d\nwq' | ${ED} -s ${WRKSRC}/common/net.h
	${ECHO_CMD} -e '9t7\n10d\nwq' | ${ED} -s ${WRKSRC}/common/net.c

post-install:
.if ${PORT_OPTIONS:MDOCS}
	@${MKDIR} ${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S,^,${WRKSRC}/,} ${DOCSDIR}
.endif

ED?=	/bin/ed

.include <bsd.port.mk>
