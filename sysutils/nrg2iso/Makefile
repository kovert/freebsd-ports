# New ports collection makefile for:   nrg2iso
# Date created:        15 Aug 2004
# Whom:                dieringe
#
# $FreeBSD$
#

PORTNAME=	nrg2iso
PORTVERSION=	0.4
CATEGORIES=	sysutils
MASTER_SITES=	http://gregory.kokanosky.free.fr/v4/linux/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Convert Nero .nrg CD-Image format to ISO

USE_GMAKE=	yes

PLIST_FILES=	bin/nrg2iso

post-patch:
	@${REINPLACE_CMD} -E \
		-e 's|gcc|${CC} ${CFLAGS}|' \
		${BUILD_WRKSRC}/${MAKEFILE}

do-install:
	@${INSTALL_PROGRAM} ${WRKSRC}/nrg2iso ${PREFIX}/bin

.include <bsd.port.mk>
