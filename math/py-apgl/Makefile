# Created by: Wen Heping <wenheping@gmail.com>
# $FreeBSD$

PORTNAME=	apgl
PORTVERSION=	0.7.3
CATEGORIES=	math python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	wen@FreeBSD.org
COMMENT=	Fast python graph library with some machine learning features

BUILD_DEPENDS=	${PYNUMPY} \
		${PYTHON_PKGNAMEPREFIX}scipy>0.7.0:${PORTSDIR}/science/py-scipy
RUN_DEPENDS:=	${BUILD_DEPENDS}

USE_PYTHON=		yes
USE_PYDISTUTILS=	easy_install

.include <bsd.port.mk>
