# New ports collection makefile for:	p5-Catalyst-Plugin-CookiedSession
# Date created:	   21 Nov 2008
# Whom:		   Denis Pokataev <catone@cpan.org>
#
# $FreeBSD$
#

PORTNAME=	Catalyst-Plugin-CookiedSession
PORTVERSION=	0.35
PORTREVISION=	1
CATEGORIES=	www perl5
MASTER_SITES=	CPAN
PKGNAMEPREFIX=	p5-

MAINTAINER=	catone@cpan.org
COMMENT=	Catalyst Plugin for storing sessions in a browser cookie

BUILD_DEPENDS=	p5-Class-Accessor>=0:${PORTSDIR}/devel/p5-Class-Accessor \
		p5-Crypt-CBC>=0:${PORTSDIR}/security/p5-Crypt-CBC \
		p5-Crypt-Rijndael>=0:${PORTSDIR}/security/p5-Crypt-Rijndael \
		p5-JSON-XS-VersionOneAndTwo>=0:${PORTSDIR}/converters/p5-JSON-XS-VersionOneAndTwo \
		p5-Catalyst-Runtime>=0:${PORTSDIR}/www/p5-Catalyst-Runtime
RUN_DEPENDS:=	${BUILD_DEPENDS}

PERL_CONFIGURE=	yes

MAN3=	Catalyst::Plugin::CookiedSession.3

.include <bsd.port.mk>
