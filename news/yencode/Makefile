# ex:ts=8
# Ports collection makefile for:	yencode
# Date created:			Mar 24, 2002
# Whom:				ijliao
#
# $FreeBSD$
#

PORTNAME=	yencode
PORTVERSION=	0.46
PORTREVISION=	6
CATEGORIES=	news
MASTER_SITES=	SF

MAINTAINER=	ports@FreeBSD.org
COMMENT=	A free (GPL) encoder and decoder for the yEnc Usenet file format

USES=		gettext
GNU_CONFIGURE=	yes

MAN1=	ydecode.1 yencode.1 ypost.1
MAN5=	ypostrc.5

CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib

.include <bsd.port.mk>
