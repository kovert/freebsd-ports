# Created by: Scott Sanders <scott@jssjr.com>
# $FreeBSD$

PORTNAME=	chef-expander
PORTVERSION=	10.24.0
CATEGORIES=	sysutils rubygems
MASTER_SITES=	RG

MAINTAINER=	ruby@FreeBSD.org
COMMENT=	A systems integration framework. Expander

RUN_DEPENDS=	rubygem-amqp=0.6.7:${PORTSDIR}/net/rubygem-amqp067 \
		rubygem-bunny>=0.6.0:${PORTSDIR}/net/rubygem-bunny \
		rubygem-em-http-request>=1.0.3:${PORTSDIR}/www/rubygem-em-http-request \
		rubygem-eventmachine>=1.0.0:${PORTSDIR}/devel/rubygem-eventmachine \
		rubygem-fast_xs>=0.7.3:${PORTSDIR}/textproc/rubygem-fast_xs \
		rubygem-highline>=1.6.1:${PORTSDIR}/devel/rubygem-highline \
		rubygem-mixlib-log>=1.2.0:${PORTSDIR}/devel/rubygem-mixlib-log \
		rubygem-uuidtools>=2.1.1:${PORTSDIR}/devel/rubygem-uuidtools \
		rubygem-yajl-ruby>=1.0:${PORTSDIR}/devel/rubygem-yajl-ruby

USE_RUBY=		yes
USE_RUBYGEMS=		yes
RUBYGEM_AUTOPLIST=	yes

PLIST_FILES=	bin/chef-expander \
		bin/chef-expander-vnode \
		bin/chef-expanderctl

.include <bsd.port.mk>
