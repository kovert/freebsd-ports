# Created by: Gea-Suan Lin <gslin@gslin.org>
# $FreeBSD$

PORTNAME=	funionfs
PORTVERSION=	0.4.3
CATEGORIES=	sysutils
MASTER_SITES=	http://funionfs.apiou.org/file/
PKGNAMEPREFIX=	fusefs-

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Union filesystem for the FUSE driver

LDFLAGS+=	-L${LOCALBASE}/lib
CFLAGS+=	-I${LOCALBASE}/include
GNU_CONFIGURE=	yes
USES=		fuse

MAN1=		funionfs.1
PLIST_FILES=	bin/funionfs

.include <bsd.port.mk>
