# New ports collection makefile for:	p5-Crypt-OFB
# Date created:				Nov 2 2003
# Whom:	      				clsung
#
# $FreeBSD$
#

PORTNAME=	Crypt-OFB
PORTVERSION=	0.01
CATEGORIES=	security perl5
MASTER_SITES=	CPAN
PKGNAMEPREFIX=	p5-

MAINTAINER=	skreuzer@FreeBSD.org
COMMENT=	Encrypt Data using OFB Mode

BUILD_DEPENDS=	p5-Crypt-ECB>=0:${PORTSDIR}/security/p5-Crypt-ECB
RUN_DEPENDS:=	${BUILD_DEPENDS}

PERL_CONFIGURE=	yes

MAN3=		Crypt::OFB.3

.include <bsd.port.mk>
