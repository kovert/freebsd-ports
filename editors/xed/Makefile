# Created by: shanee
# $FreeBSD$

PORTNAME=	xed
PORTVERSION=	1.3
PORTREVISION=	2
CATEGORIES=	editors
MASTER_SITES=	${MASTER_SITE_XCONTRIB}
MASTER_SITE_SUBDIR=	editors
DISTNAME=	${PORTNAME}${PORTVERSION}
EXTRACT_SUFX=	.tar.Z

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Text editor for X

USES=		imake
USE_XORG=	xaw
MAN1=		xed.1

pre-build:
	@${FIND} ${WRKSRC} -type f | ${XARGS} ${REINPLACE_CMD} -e \
		's|extern char \*malloc();|/\* extern char \*malloc(); \*/|g'
.include <bsd.port.mk>
