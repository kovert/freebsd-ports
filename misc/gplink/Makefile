# Created by: king@v2project.com
# $FreeBSD$

PORTNAME=	gplink
PORTVERSION=	1.5
CATEGORIES=	misc
MASTER_SITES=	http://gp2x.org/gp32/gplink/ \
		http://www.gnu-darwin.org/distfiles/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	GP32 USB linker tool

LICENSE=	GPLv2 GPLv3
LICENSE_COMB=	dual

WRKSRC=		${WRKDIR}/${DISTNAME}/src

USE_GMAKE=	yes
MAKE_ARGS=	CC="${CC}" \
		CFLAGS="${CFLAGS} ${USB_CFLAGS}" \
		LDFLAGS="${USB_LDFLAGS}"
MAKE_JOBS_SAFE=	yes

PLIST_FILES=	bin/gplink

.include <bsd.port.pre.mk>

USB_CFLAGS=	# none
USB_LDFLAGS=	-lusb

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/gplink ${PREFIX}/bin

.include <bsd.port.post.mk>
