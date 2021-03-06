# New ports collection makefile for:	nehquake
# Date created:				16 May 2006
# Whom:					alepulver
#
# $FreeBSD$
#

PORTNAME=	nehquake
PORTVERSION=	1.0
PORTREVISION=	5
CATEGORIES=	games
MASTER_SITES=	${MASTER_SITE_LOCAL}
MASTER_SITE_SUBDIR=	alepulver
DISTNAME=	NehQuake-bjp-bin-src.linux

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Quake engine designed for playing Nehahra

USE_BZIP2=	yes
USE_DOS2UNIX=	yes
USE_GL=		gl
USE_XORG=	xxf86dga
USE_GMAKE=	yes

OPTIONS_DEFINE=	OPTIMIZED_CFLAGS SDL X86_ASM
OPTIONS_DEFAULT=	OPTIMIZED_CFLAGS SDL X86_ASM
X86_ASM_DESC=	Enable x86 assembly code

ALL_TARGET=	release
SUB_FILES=	pkg-message

.include "${.CURDIR}/../quake-data/Makefile.include"

.include <bsd.port.options.mk>

.for f in OPTIMIZED_CFLAGS X86_ASM
.   if ${PORT_OPTIONS:M${f}}
MAKE_ENV+=	USE_${f}=YES
.   else
MAKE_ENV+=	USE_${f}=NO
.   endif
.endfor

.if ${PORT_OPTIONS:MSDL}
USE_SDL=	sdl
MAKE_ENV+=	BUILD_SDL=YES
PLIST_SUB+=	SDL=""
.else
PLIST_SUB+=	SDL="@comment "
.endif

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/release/nehahra ${PREFIX}/bin
.if ${PORT_OPTIONS:MSDL}
	${INSTALL_PROGRAM} ${WRKSRC}/release/nehahra-sdl ${PREFIX}/bin
.endif
	${MKDIR} ${Q1DIR}/nehahra

post-install:
	@${ECHO_CMD}
	@${CAT} ${PKGMESSAGE}
	@${ECHO_CMD}

.include <bsd.port.mk>
