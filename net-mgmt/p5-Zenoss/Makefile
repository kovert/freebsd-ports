# New ports collection makefile for:    p5-Zenoss
# Date created:                         25 August 2011
# Whom:                                 Phil Phillips
#
# $FreeBSD$
#

PORTNAME=	Zenoss
PORTVERSION=	1.11
CATEGORIES=	net-mgmt perl5
MASTER_SITES=	CPAN
PKGNAMEPREFIX=	p5-

MAINTAINER=	pphillips@experts-exchange.com
COMMENT=	Perl interface to the Zenoss JSON API

BUILD_DEPENDS=	p5-HTTP-Message>=0:${PORTSDIR}/www/p5-HTTP-Message \
		p5-JSON>=2.0:${PORTSDIR}/converters/p5-JSON \
		p5-Moose>=1.0:${PORTSDIR}/devel/p5-Moose \
		p5-libwww>=5.0:${PORTSDIR}/www/p5-libwww
RUN_DEPENDS=	p5-HTTP-Message>=0:${PORTSDIR}/www/p5-HTTP-Message \
		p5-JSON>=2.0:${PORTSDIR}/converters/p5-JSON \
		p5-Moose>=1.0:${PORTSDIR}/devel/p5-Moose \
		p5-libwww>=5.0:${PORTSDIR}/www/p5-libwww

PERL_CONFIGURE=	yes

MAN3=		Zenoss.3 \
		Zenoss::Connector.3 \
		Zenoss::Error.3 \
		Zenoss::Examples.3 \
		Zenoss::MetaHelper.3 \
		Zenoss::Response.3 \
		Zenoss::Router.3 \
		Zenoss::Router::DetailNav.3 \
		Zenoss::Router::Device.3 \
		Zenoss::Router::Events.3 \
		Zenoss::Router::Messaging.3 \
		Zenoss::Router::Mib.3 \
		Zenoss::Router::Network.3 \
		Zenoss::Router::Process.3 \
		Zenoss::Router::Report.3 \
		Zenoss::Router::Search.3 \
		Zenoss::Router::Service.3 \
		Zenoss::Router::Template.3 \
		Zenoss::Router::Tree.3 \
		Zenoss::Router::ZenPack.3

.include <bsd.port.mk>
