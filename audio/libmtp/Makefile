# Created by: Petar Zhivkov Petrov <pesho.petrov@gmail.com>
# $FreeBSD$

PORTNAME=	libmtp
PORTVERSION=	1.1.6
PORTREVISION=	1
CATEGORIES=	audio
MASTER_SITES=	SF

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Media Transfer Protocol (MTP) library

LICENSE=	LGPL21

OPTIONS_DEFINE=	MTPZ
OPTIONS_DEFAULT=	MTPZ
MTPZ_DESC=	Enable functionality to connect to MTPZ devices

USES=		pathfix pkgconfig iconv
GNU_CONFIGURE=	yes
USE_LDCONFIG=	yes
MAKE_JOBS_SAFE=	yes

CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MMTPZ}
LIB_DEPENDS+=	gcrypt:${PORTSDIR}/security/libgcrypt
.else
CONFIGURE_ARGS+=--disable-mtpz
.endif

.include <bsd.port.pre.mk>

CONFIGURE_ENV+=	LIBUSB_CFLAGS="-I/usr/include" LIBUSB_LIBS="-lusb" LIBS="-lusb"

post-patch:
	@${REINPLACE_CMD} -e \
		'/^SUBDIRS/s|doc||' ${WRKSRC}/Makefile.in
	@${REINPLACE_CMD} -e \
		'/if test/s|==|=| ; \
		 /LIBUSB_REQUIRES/s|libusb-1.0|| ; \
		 /endian.h/s|machine|sys|' ${WRKSRC}/configure
	@${REINPLACE_CMD} -e \
		's|<libusb-1.0/|<|' ${WRKSRC}/src/libusb-glue.h
	@${REINPLACE_CMD} -e \
		's|__builtin_bswap|bswap|g' ${WRKSRC}/src/mtpz.c

.include <bsd.port.post.mk>
