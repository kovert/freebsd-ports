# Created by: Alejandro Pulver <alepulver@FreeBSD.org>
# $FreeBSD$

PORTNAME=	quake2max
PORTVERSION=	0.45
PORTREVISION=	8
CATEGORIES=	games
MASTER_SITES=	http://www.bfeared.com/library/quake/archive/quakedev/qudos/quake2/engines/Quake2MaX/:src \
		${MASTER_SITE_LOCAL:S/$/:data/}
MASTER_SITE_SUBDIR=	alepulver/:data
DISTNAME=	Quake2maX_${PORTVERSION}-src_unix
DISTFILES=	${DISTNAME}${EXTRACT_SUFX}:src \
		${Q2MAX_DATA}:data
EXTRACT_ONLY=	${DISTNAME}${EXTRACT_SUFX}

MAINTAINER=	danfe@FreeBSD.org
COMMENT=	OpenGL-only Quake II engine modification

LICENSE=	GPLv2

EXTRACT_DEPENDS=	unrar:${PORTSDIR}/archivers/unrar

USE_BZIP2=	yes
USE_GMAKE=	yes
USE_XORG=	xxf86dga
ALL_TARGET=	release
WRKSRC=		${WRKDIR}/${DISTNAME:S/quake2max/Quake2maX/}

LIBDIR=		${PREFIX}/lib/${PORTNAME}
MAKE_ENV=	LIBDIR="${LIBDIR}"
PLIST_SUB=	LIBDIR="${LIBDIR:S/${PREFIX}\///}"

Q2MAX_DATA=	${PORTNAME}.044.rar

OPTIONS_DEFINE=	CLIENT DEDICATED GAME GLX OPTIMIZED_CFLAGS SDLCLIENT SDLGL
OPTIONS_DEFAULT=	CLIENT DEDICATED GLX OPTIMIZED_CFLAGS SDLCLIENT SDLGL

CLIENT_DESC=	Build original client
DEDICATED_DESC=	Build dedicated server
GAME_DESC=	Build main game (default mod)
GLX_DESC=	Build OpenGL renderer
SDLCLIENT_DESC=	Build SDL client
SDLGL_DESC=	Build SDL OpenGL renderer

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MGLX} || ${PORT_OPTIONS:MSDLGL}
LIB_DEPENDS=	jpeg:${PORTSDIR}/graphics/jpeg \
		png15:${PORTSDIR}/graphics/png
USE_GL=		glu
.endif

.if ${PORT_OPTIONS:MSDLCLIENT} || ${PORT_OPTIONS:MSDLGL}
USE_SDL=	yes
.endif

.if ${PORT_OPTIONS:MCLIENT}
MAKE_ENV+=	BUILD_QUAKE2MAX=YES
PLIST_SUB+=	CLIENT=""
Q2MAX_BIN+=	quake2max
.else
PLIST_SUB+=	CLIENT="@comment "
.endif

.if ${PORT_OPTIONS:MDEDICATED}
MAKE_ENV+=	BUILD_DEDICATED=YES
PLIST_SUB+=	DEDICATED=""
Q2MAX_BIN+=	quake2max-ded
.else
PLIST_SUB+=	DEDICATED="@comment "
.endif

.if ${PORT_OPTIONS:MGAME}
MAKE_ENV+=	BUILD_GAME=YES
PLIST_SUB+=	GAME=""
.else
PLIST_SUB+=	GAME="@comment "
.endif

.if ${PORT_OPTIONS:MGLX}
MAKE_ENV+=	BUILD_GLX=YES
PLIST_SUB+=	GLX=""
Q2MAX_REF+=	glx
.else
PLIST_SUB+=	GLX="@comment "
.endif

.if ${PORT_OPTIONS:MOPTIMIZED_CFLAGS}
MAKE_ENV+=	WITH_OPTIMIZED_CFLAGS=YES
.endif

.if ${PORT_OPTIONS:MSDLCLIENT}
MAKE_ENV+=	BUILD_QUAKE2MAX-SDL=YES
PLIST_SUB+=	SDLCLIENT=""
Q2MAX_BIN+=	quake2max-sdl
.else
PLIST_SUB+=	SDLCLIENT="@comment "
.endif

.if ${PORT_OPTIONS:MSDLGL}
MAKE_ENV+=	BUILD_SDLGL=YES
PLIST_SUB+=	SDLGL=""
Q2MAX_REF+=	sdlgl
.else
PLIST_SUB+=	SDLGL="@comment "
.endif

post-extract:
	@cd ${WRKSRC} && unrar e -idq ${DISTDIR}/${Q2MAX_DATA} \
		baseq2/_maxpak.pak

post-patch:
# Resolve name collision with jpeg-8
	@${REINPLACE_CMD} -e 's|jpeg_mem_src|local_jpeg_mem_src|' \
		${WRKSRC}/ref_gl/gl_image.c

do-install:
	@${MKDIR} ${LIBDIR}/baseq2
.for f in ${Q2MAX_BIN}
	${INSTALL_PROGRAM} ${WRKSRC}/quake2/${f} ${PREFIX}/bin
.endfor
.for f in ${Q2MAX_REF}
	${INSTALL_PROGRAM} ${WRKSRC}/quake2/rfx_${f}.so ${LIBDIR}
.endfor
.if ${PORT_OPTIONS:MGAME}
	${INSTALL_PROGRAM} ${WRKSRC}/quake2/baseq2/game.so ${LIBDIR}/baseq2
.endif
	${INSTALL_DATA} ${WRKSRC}/_maxpak.pak ${LIBDIR}/baseq2/maxpak.pak

.include "${.CURDIR}/../quake2-data/Makefile.include"
.include <bsd.port.mk>
