# Created by: johnpupu <johnpupu@gmail.com>
# $FreeBSD$

PORTNAME=	Net-POP3-SSLWrapper
PORTVERSION=	0.06
CATEGORIES=	mail perl5
MASTER_SITES=	CPAN
PKGNAMEPREFIX=	p5-

MAINTAINER=	johnpupu@gmail.com
COMMENT=	Perl extension for simple POP3S wrapper for Net::POP3

BUILD_DEPENDS=	p5-IO-Socket-SSL>=1.34:${PORTSDIR}/security/p5-IO-Socket-SSL
RUN_DEPENDS=	p5-IO-Socket-SSL>=1.34:${PORTSDIR}/security/p5-IO-Socket-SSL

PERL_CONFIGURE=	yes

MAN3=		Net::POP3::SSLWrapper.3

.include <bsd.port.mk>
