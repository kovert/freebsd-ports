# Ports collection makefile for:  Ingo
# Date created:			  Dec 3, 2004
# Whom:				  Thierry Thomas (<thierry@pompo.net>)
#
# $FreeBSD$
#

PORTNAME=	ingo
PORTVERSION=	1.2.6
DISTVERSIONSUFFIX=
PORTREVISION=	1
PORTEPOCH=	1
CATEGORIES=	mail www

MAINTAINER=	horde@FreeBSD.org
COMMENT=	Email-filter management application

#-----------------------------------------------------------------------
# You may define this option:
#
# - WITH_SIEVE	: if you run timsieved (with Cyrus).
#
#-----------------------------------------------------------------------

.if defined(WITH_SIEVE) || exists(${LOCALBASE}/cyrus/bin/timsieved)
RUN_DEPENDS+=	${PEARDIR}/Net/Sieve.php:${PORTSDIR}/net/pear-Net_Sieve
.endif

USE_PHP=	imap
USE_HORDE=	base pkg-message
USES=		gettext
PORTDOCS=	README CHANGES CREDITS INSTALL RELEASE_NOTES TODO

.include "${.CURDIR}/../../www/horde3-base/bsd.horde.mk"
.include <bsd.port.mk>
