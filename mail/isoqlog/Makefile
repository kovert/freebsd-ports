# New ports collection makefile for:   isoqlog
# Date created:                 17 June 2002
# Whom:				ofsen@enderunix.org
#
# $FreeBSD$
#

PORTNAME=	isoqlog
PORTVERSION=	2.2.1
PORTREVISION=	1
CATEGORIES=	mail
MASTER_SITES=	http://www.enderunix.org/isoqlog/ \
		http://www.trunix.org/projeler/isoqlog/ \
		http://www.acikkod.org/softwares/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	A qmail, postfix, sendmail, exim MTA log analysis program

GNU_CONFIGURE=	yes
USE_GMAKE=	yes

SUB_FILES=	pkg-message

.include <bsd.port.pre.mk>

.ifdef NOPORTDOCS
post-patch:
	@${REINPLACE_CMD} -e '/install-data-am:/s/install-${PORTNAME}_docDATA//' \
			-e '/SUBDIRS = /s/tr//' \
		${WRKSRC}/Makefile.in
.endif

post-install:
	@${CAT} ${PKGMESSAGE}

.include <bsd.port.post.mk>
