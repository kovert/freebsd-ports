# Created by: Raphael Kubo da Costa <rakuco@FreeBSD.org>
# $FreeBSD$

PORTNAME=	dragon
PORTVERSION=	${KDE4_VERSION}
CATEGORIES=	multimedia kde
MASTER_SITES=	${MASTER_SITE_KDE}
MASTER_SITE_SUBDIR=	${KDE4_BRANCH}/${PORTVERSION}/src
DIST_SUBDIR=	KDE/${PORTVERSION}

MAINTAINER=	kde@FreeBSD.org
COMMENT=	KDE multimedia player with a focus on simplicity

LICENSE=	GPLv2

# Avoid clash with devel/dragon
LATEST_LINK=	kdemultimedia-dragon
CONFLICTS_INSTALL=	kdemultimedia-4.[1-8].*

USES=		cmake:outsource
USE_KDE4=	automoc4 kdehier kdelibs kdeprefix
USE_QT4=	phonon moc_build qmake_build rcc_build uic_build
USE_XZ=		yes
MAKE_JOBS_SAFE=	yes

MAN1=		dragon.1

post-install:
	@${CAT} ${PKGMESSAGE}

.include <bsd.port.mk>
