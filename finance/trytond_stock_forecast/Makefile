# $FreeBSD$

PORTNAME=	trytond_stock_forecast
PORTVERSION=	2.4.0
PORTREVISION=	1
CATEGORIES=	finance python
MASTER_SITES=	http://downloads.tryton.org/${PORTVERSION:R}/

MAINTAINER=	matthias@petermann.it
COMMENT=	Tryton Application Platform (Stock Forecast Module)

LICENSE=	GPLv3

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}dateutil>=1.5:${PORTSDIR}/devel/py-dateutil \
		trytond>=2.4.0:${PORTSDIR}/finance/trytond \
		trytond_product>=2.4.0:${PORTSDIR}/finance/trytond_product \
		trytond_stock>=2.4.0:${PORTSDIR}/finance/trytond_stock \
		trytond_company>=2.4.0:${PORTSDIR}/finance/trytond_company

CONFLICTS=	trytond_stock_forecast-2.[68].*

USE_PYTHON=	yes
USE_PYDISTUTILS=easy_install

.include <bsd.port.mk>
