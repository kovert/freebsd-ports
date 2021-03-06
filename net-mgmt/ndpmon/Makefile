# Created by: janos.mohacsi@bsd.hu
# $FreeBSD$

PORTNAME=	ndpmon
PORTVERSION=	1.4.0
PORTREVISION=	2
CATEGORIES=	net-mgmt ipv6
MASTER_SITES=	SF/${PORTNAME}/${PORTNAME}/${PORTNAME}-1.4/
EXTRACT_SUFX=	.tgz

MAINTAINER=	jmohacsi@bsd.hu
COMMENT=	On-link icmpv6 message monitoring and reporting daemon

LICENSE=	LGPL21
LICENSE_FILE=	${WRKSRC}/COPYING

OPTIONS_DEFINE=		PY4SUITE MACRESOLV
OPTIONS_DEFAULT=	

PY4SUITE_DESC=		Depend on py-4suite-xml (for generating HTML)
MACRESOLV_DESC=		Enable MAC Manufacturer Resolution (use p5-libwww)

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MPY4SUITE}
RUN_DEPENDS+=	${PYTHON_SITELIBDIR}/Ft/Xml/Domlette.py:${PORTSDIR}/textproc/py-4suite-xml
USE_PYTHON=	2.6+
PLIST_SUB+=	PY=""
.else
PLIST_SUB+=	PY="@comment "
.endif

USE_GNOME=	libxml2
USE_PERL5_RUN=	yes
USE_RC_SUBR=	ndpmonitor

MAKE_JOBS_SAFE=	yes
GNU_CONFIGURE=	yes
CONFIGURE_ENV=	OSTYPE=FreeBSD
CONFIGURE_ARGS=	--with-var-datadir=${PREFIX}/var --with-confdir=${ETCDIR} \
		--with-libxml2=${LOCALBASE} --cache-file=/dev/null

MAN8=		ndpmon.8
PORTDOCS=	INSTALL README

.if ${PORT_OPTIONS:MMACRESOLV}
CONFIGURE_ARGS+=--enable-mac-resolv
BUILD_DEPENDS+=	p5-libwww>=6.05:${PORTSDIR}/www/p5-libwww
RUN_DEPENDS+=	p5-libwww>=6.05:${PORTSDIR}/www/p5-libwww
PLIST_SUB+=	MACRESOLV=""
.else
PLIST_SUB+=	MACRESOLV="@comment "
.endif

post-patch:
	@${REINPLACE_CMD} -e 's|%%PREFIX%%|${PREFIX}|g' \
		-e 's|%%LOCALBASE%%|${LOCALBASE}|g' \
		${WRKSRC}/ndpmon.8 \
		${WRKSRC}/create_html_table.py \
		${WRKSRC}/demopipeprogram.pl.sample \
		${WRKSRC}/config_ndpmon.xml.in \
		${WRKSRC}/config_ndpmon.xml
	(cd ${WRKSRC}; ${MAKE} clean)

do-install:
	${INSTALL_MAN} ${WRKSRC}/ndpmon.8 ${PREFIX}/man/man8
	${INSTALL_PROGRAM} ${WRKSRC}/ndpmon ${PREFIX}/sbin

	${MKDIR} ${DATADIR}
	${INSTALL_DATA} ${WRKSRC}/*.dtd ${DATADIR}
	${INSTALL_SCRIPT} ${WRKSRC}/demopipeprogram.pl.sample ${DATADIR}
.if ${PORT_OPTIONS:MPY4SUITE}
	${INSTALL_SCRIPT} ${WRKSRC}/create_html_table.py ${DATADIR}
.endif
.if ${PORT_OPTIONS:MMACRESOLV}
	${MKDIR} ${DATADIR}/plugins/mac_resolv
	${INSTALL_SCRIPT} ${WRKSRC}/plugins/mac_resolv/make-manuf ${DATADIR}/plugins/mac_resolv
	${INSTALL_DATA} ${WRKSRC}/plugins/mac_resolv/*.tmpl ${DATADIR}/plugins/mac_resolv
	${INSTALL_DATA} ${WRKSRC}/plugins/mac_resolv/manuf ${DATADIR}/plugins/mac_resolv
.endif

	${MKDIR} ${ETCDIR}
	${INSTALL_DATA} ${WRKSRC}/config_ndpmon.xml ${ETCDIR}/config_ndpmon.xml-dist

	${MKDIR} ${PREFIX}/var/ndpmon
	${INSTALL_DATA} ${WRKSRC}/neighbor_list.xml ${PREFIX}/var/ndpmon/neighbor_list.xml

.if ${PORT_OPTIONS:MDOCS}
post-install:
	${MKDIR} ${DOCSDIR}
	cd ${WRKSRC} && ${INSTALL_DATA} ${PORTDOCS} ${DOCSDIR}
.endif
.if ${PORT_OPTIONS:MMACRESOLV}
	@${CAT} ${PKGMESSAGE}.MACRESOLV
.endif

.include <bsd.port.mk>
