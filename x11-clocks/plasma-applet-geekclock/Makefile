# New ports collection makefile for:	plasma-applet-geekclock
# Date Created:				2009-07-08
# Whom:					Jason E. Hale <bsdkaffee@gmail.com>
#
# $FreeBSD$
#

PORTNAME=	geekclock
PORTVERSION=	1.0
PORTREVISION=	7
CATEGORIES=	x11-clocks deskutils kde
MASTER_SITES=	http://w2f2.com/projects/${PORTNAME}/
PKGNAMEPREFIX=	plasma-applet-
DISTNAME=	geek-clock-plasmoid-${PORTVERSION}-src

MAINTAINER=	jhale@FreeBSD.org
COMMENT=	Geeky analog clock plasma applet for KDE4

USES=		cmake
USE_KDE4=	automoc4 kdeprefix kdelibs workspace
USE_QT4=	gui dbus network opengl svg webkit xml \
		qmake_build moc_build rcc_build uic_build
MAKE_JOBS_SAFE=	yes

PLIST_FILES=	lib/kde4/plasma_applet_geekclock.so \
		share/apps/desktoptheme/default/widgets/geekclock.svgz \
		share/kde4/services/plasma-applet-geekclock.desktop

.include <bsd.port.mk>
