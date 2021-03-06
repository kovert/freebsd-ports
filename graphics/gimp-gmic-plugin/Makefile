# Created by: Mahmatkhanov Ruslan <cvs-src@yandex.ru>
# $FreeBSD$

PORTNAME=	gmic
PORTVERSION=	1.5.5.2
CATEGORIES=	graphics
MASTER_SITES=	SF/${PORTNAME} \
		SF/${PORTNAME}/old
PKGNAMEPREFIX=	gimp-
PKGNAMESUFFIX=	-plugin
DISTNAME=	${PORTNAME}_${PORTVERSION}

MAINTAINER=	rm@FreeBSD.org
COMMENT=	GREYC's Magic Image Converter

LIB_DEPENDS=	GraphicsMagick++.9:${PORTSDIR}/graphics/GraphicsMagick13 \
		IlmImf:${PORTSDIR}/graphics/OpenEXR \
		Magick++:${PORTSDIR}/graphics/ImageMagick \
		avcodec.1:${PORTSDIR}/multimedia/ffmpeg \
		fftw3:${PORTSDIR}/math/fftw3 \
		gimp-2.0:${PORTSDIR}/graphics/gimp-app

OPTIONS_DEFINE=	BASH
BASH_DESC=	Install programmable completions for Bash
OPTIONS_EXCLUDE=NLS DOCS

WRKSRC=		${WRKDIR}/${PORTNAME}-${PORTVERSION}/src

USE_GMAKE=	yes
USE_GNOME=	gtk20
USE_XORG=	x11 xext xrandr

PLUGIN_DIR?=	libexec/gimp/2.2/plug-ins
PLIST_SUB+=	PLUGIN_DIR=${PLUGIN_DIR}

CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib
CFLAGS:=	${CFLAGS:N-O*:N-pipe}
CXXFLAGS:=	${CXXFLAGS:N-O*:N-pipe}

MAN1=		gmic.1
MANCOMPRESSED=	yes

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MBASH}
RUN_DEPENDS+=	${LOCALBASE}/bin/bash:${PORTSDIR}/shells/bash
PLIST_SUB+=	BASH=""
.else
PLIST_SUB+=	BASH="@comment "
.endif

post-patch:
	@${REINPLACE_CMD} -e 's#/usr/X11R6#${PREFIX}#g' \
		${WRKSRC}/Makefile

do-install:
	@${MKDIR} ${PREFIX}/${PLUGIN_DIR}
	${INSTALL_PROGRAM} ${WRKSRC}/gmic_gimp ${PREFIX}/${PLUGIN_DIR}
	${INSTALL_PROGRAM} ${WRKSRC}/gmic ${PREFIX}/bin
	${INSTALL_MAN} ${WRKSRC}/../man/gmic.1.gz ${MAN1PREFIX}/man/man1
.if ${PORT_OPTIONS:MBASH}
	${INSTALL_SCRIPT} ${WRKSRC}/gmic_bashcompletion.sh \
		${PREFIX}/etc/bash_completion.d/gmic_bashcompletion.sh
.endif

.include <bsd.port.mk>
