# Created by: Kyle Martin <mkm@ieee.org>
# $FreeBSD$

PORTNAME=	cmake
PORTVERSION=	2.8.11.2
CATEGORIES=	devel
MASTER_SITES=	http://www.cmake.org/files/v2.8/

MAINTAINER=	kde@FreeBSD.org
COMMENT?=	Cross-platform Makefile generator

LICENSE=	BSD

CONFIGURE_ENV=	MAKE=make
CONFIGURE_ARGS=	--prefix=${PREFIX} \
		--datadir="/${DATADIR_REL}" \
		--docdir="/${DOCSDIR_REL}"
MAKE_JOBS_SAFE=	yes

.if defined(STRIP) && ${STRIP} != ""
INSTALL_TARGET=	install/strip
.endif

.if !defined(CMAKE_MODULES)
HAS_CONFIGURE=	yes
RUN_DEPENDS=	${DATADIR}/Modules/CMake.cmake:${PORTSDIR}/devel/cmake-modules

MAN1=		ccmake.1 \
		cmake.1 \
		cmakecommands.1 \
		cmakecompat.1 \
		cmakemodules.1 \
		cmakepolicies.1	\
		cmakeprops.1 \
		cmakevars.1 \
		cpack.1 \
		ctest.1
.endif

post-patch:
	@(${FIND} ${WRKSRC}/Modules -name "*.cmake" -print0; \
		${FIND} ${WRKSRC}/Tests -name "CMakeLists.txt" -print0 ) | \
		${XARGS} -0 -n 100 ${REINPLACE_CMD} -e 's,/usr/local,${LOCALBASE},g; \
			s,/usr/X11R6,${LOCALBASE},g'
	@${REINPLACE_CMD} -e 's,/usr/local,${LOCALBASE},g' \
		${WRKSRC}/Source/cmLocalGenerator.cxx \
		${WRKSRC}/Source/CPack/cmCPackGenerator.cxx \
		${WRKSRC}/bootstrap
	@${REINPLACE_CMD} -e 's,/opt/kde4,${LOCALBASE}/kde4,g' \
		${WRKSRC}/Modules/FindKDE4.cmake
	@${REINPLACE_CMD} -e 's,/usr/include,${LOCALBASE}/include,' \
	   	${WRKSRC}/Modules/FindDCMTK.cmake
	@${FIND} ${WRKSRC} -name "*.bak" -delete -o -name "*.orig" -delete

.if !defined(CMAKE_MODULES)
post-install:
	${INSTALL_DATA} ${WRKSRC}/Docs/cmake-mode.el ${PREFIX}/share/emacs/site-lisp
.endif

.include <bsd.port.mk>
