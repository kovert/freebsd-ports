# Created by: Denis Shaposhnikov <dsh@vlink.ru>
# $FreeBSD$

PORTNAME=	tkabber
PORTVERSION=	0.11.1.a.20100207
PORTREVISION=	1
CATEGORIES=	net-im
MASTER_SITES=	http://wizard.volgograd.ru/distfiles/
PKGNAMESUFFIX=	-devel

MAINTAINER=	dsh@wizard.volgograd.ru
COMMENT=	Tcl/Tk based jabber client, development version

LIB_DEPENDS=	tkXwin.1:${PORTSDIR}/x11/tkXwin
RUN_DEPENDS=	tcllib>=1.10:${PORTSDIR}/devel/tcllib \
		tcltls>=1.5.0:${PORTSDIR}/devel/tcltls \
		bwidget>=1.8.0:${PORTSDIR}/x11-toolkits/bwidget

CONFLICTS=	tkabber-[0-9]*
NO_BUILD=	yes
WRKSRC=		${WRKDIR}/${PORTNAME}

USE_BZIP2=	yes
USE_TCL_RUN=	85+
USE_TK_RUN=	85+

DESKTOP_ENTRIES=	"${PORTNAME}" \
		"${COMMENT}" \
		"" \
		"tkabber" \
		"Network;InstantMessaging;" \
		false

SUBDIRS=	emoticons ifacetk mclistbox msgs pixmaps plugins sounds \
		tclxmpp trans

OPTIONS_DEFINE=	ZLIB

.include <bsd.port.options.mk>

do-install:
	${ECHO} -e "#!/bin/sh\nexec ${WISH} ${DATADIR}/tkabber.tcl \
		-name tkabber \"\$$@\"\n" > ${WRKDIR}/tkabber.sh
	${INSTALL_SCRIPT} ${WRKDIR}/tkabber.sh ${PREFIX}/bin/tkabber

	${ECHO} -e "#!/bin/sh\nexec ${TCLSH} ${DATADIR}/tkabber-remote.tcl \
		-name tkabber-remote \"\$$@\"\n" > ${WRKDIR}/tkabber-remote.sh
	${INSTALL_SCRIPT} ${WRKDIR}/tkabber-remote.sh ${PREFIX}/bin/tkabber-remote

	${MKDIR} ${DATADIR}
	${INSTALL_DATA} ${WRKSRC}/*.tcl ${DATADIR}
	(cd ${WRKSRC} && ${COPYTREE_SHARE} "${SUBDIRS}" ${DATADIR})
	${HEAD} -1 ${WRKSRC}/ChangeLog > ${DATADIR}/version

	${MKDIR} ${EXAMPLESDIR}
	(cd ${WRKSRC}/examples && ${COPYTREE_SHARE} \* ${EXAMPLESDIR})

.if ${PORT_OPTIONS:MDOCS}
	${MKDIR} ${DOCSDIR}
.  for i in AUTHORS COPYING ChangeLog README
	${INSTALL_DATA} ${WRKSRC}/${i} ${DOCSDIR}
.  endfor
	${INSTALL_DATA} ${WRKSRC}/doc/* ${DOCSDIR}
.endif

.if ${PORT_OPTIONS:MZLIB}
LIB_DEPENDS+=	ztcl[0-9]:${PORTSDIR}/devel/ztcl
.endif

.include <bsd.port.mk>
