# Created by: stb
# $FreeBSD$

PORTNAME=	netatalk
PORTVERSION=	3.0.4
PORTEPOCH=	1
CATEGORIES=	net
MASTER_SITES=	SF

MAINTAINER=	marcus@FreeBSD.org
COMMENT=	File server for Mac OS X

LIB_DEPENDS=	gcrypt:${PORTSDIR}/security/libgcrypt \
    		event-2:${PORTSDIR}/devel/libevent2

LATEST_LINK=	netatalk3
USE_AUTOTOOLS=	libtool
USE_BDB=	46+
USE_BZIP2=	yes
USES=		iconv
GNU_CONFIGURE=	yes
USE_GMAKE=	yes
USE_PERL5=	yes
USE_GNOME=	pkgconfig
WANT_GNOME=	yes
USE_LDCONFIG=	yes
USE_RC_SUBR=	netatalk

CONFIGURE_ARGS+=	--enable-tcp-wrappers \
			--with-pkgconfdir=${PREFIX}/etc \
			--with-libiconv=${LOCALBASE} \
			--with-libgcrypt-dir=${LOCALBASE} \
			--with-uams-path=${PREFIX}/libexec/netatalk-uams \
			--with-bdb=${LOCALBASE} \
			--localstatedir=/var \
			--disable-bundled-libevent \
			--with-libevent-header=${LOCALBASE}/include \
			--with-libevent-lib=${LOCALBASE}/lib/event2

OPTIONS_DEFINE=PAM KRB5 ZEROCONF LDAP SENDFILE KERBEROS DTRACE DBUS
OPTIONS_DEFAULT=ZEROCONF KERBEROS DBUS

ZEROCONF_DESC=	Enable Zeroconf (Bonjour) support
KRB5_DESC=	Enable Kerberos V UAM
DTRACE_DESC=	Enable DTrace support
SENDFILE_DESC=	Enable Sendfile support

.include <bsd.port.options.mk>

MAN1=		ad.1 afpldaptest.1 afppasswd.1 apple_dump.1 asip-status.pl.1 \
		dbd.1 macusers.1 netatalk-config.1 uniconv.1
MAN5=		afp.conf.5 afp_signature.conf.5 afp_voluuid.conf.5 \
		extmap.conf.5
MAN8=		afpd.8 cnid_dbd.8 cnid_metad.8 netatalk.8

CONFLICTS=	bigloo-2.* cap-6.0.* tct-1.* netatalk-[12]* yudit-[0-9]*

.include <bsd.port.pre.mk>

.if ${PORT_OPTIONS:MKRB5}
CONFIGURE_ARGS+=	--enable-krbV-uam
PLIST_SUB+=		NETATALKKRB5=""
.else
PLIST_SUB+=		NETATALKKRB5="@comment "
.endif

.if ${PORT_OPTIONS:MDTRACE}
CONFIGURE_ARGS+=	--with-dtrace
.else
CONFIGURE_ARGS+=	--without-dtrace
.endif

.if ${PORT_OPTIONS:MKERBEROS}
CONFIGURE_ARGS+=	--with-kerberos
.else
CONFIGURE_ARGS+=	--without-kerberos
.endif

.if ${PORT_OPTIONS:MPAM}
CONFIGURE_ARGS+=	--with-pam
PLIST_SUB+=		NETATALKPAM=""
.else
CONFIGURE_ARGS+=	--without-pam
PLIST_SUB+=		NETATALKPAM="@comment "
.endif

.if ${PORT_OPTIONS:MZEROCONF}
CONFIGURE_ARGS+=	--enable-zeroconf=${LOCALBASE}
CFLAGS+=		-I${LOCALBASE}/include -L${LOCALBASE}/lib
LIB_DEPENDS+=		avahi-client:${PORTSDIR}/net/avahi-app
USE_GNOME+=		pkgconfig
SUB_LIST+=		ZEROCONF="avahi_daemon"
.else
CONFIGURE_ARGS+=	--disable-zerconf
SUB_LIST+=		ZEROCONF=""
.endif

.if ${PORT_OPTIONS:MLDAP}
CONFIGURE_ARGS+=	--with-ldap=${LOCALBASE}
CFLAGS+=		-I${LOCALBASE}/include -L${LOCALBASE}/lib
USE_OPENLDAP=		yes
.else
CONFIGURE_ARGS+=	--without-ldap
.endif

.if ${PORT_OPTIONS:MSENDFILE}
CONFIGURE_ARGS+=	--enable-sendfile
.else
CONFIGURE_ARGS+=	--disable-sendfile
.endif

.if ${PORT_OPTIONS:MDBUS} || exists(${LOCALBASE}/libdata/pkgconfig/dbus-glib-1.pc)
LIB_DEPENDS+=		dbus-glib-1:${PORTSDIR}/devel/dbus-glib
RUN_DEPENDS+=		${LOCALBASE}/libdata/pkgconfig/dbus-python.pc:${PORTSDIR}/devel/py-dbus
PLIST_SUB+=		DBUS=""
MAN1+=			afpstats.1
.else
PLIST_SUB+=		DBUS="@comment "
.endif

.if ${OSVERSION} < 800031
PLIST_SUB+=	ATFUNCS="@comment "
.else
PLIST_SUB+=	ATFUNCS=""
.endif

post-patch:
	@${REINPLACE_CMD} -e 's|%%DB_NAME%%|${BDB_INCLUDE_DIR:T}| ; \
	    	s|%%DB_LIB%%|-l${BDB_LIB_NAME}|g ; \
		s|%%LOCALBASE%%|${LOCALBASE}|g' \
		${WRKSRC}/configure

post-install:
	${INSTALL_SCRIPT} ${WRKSRC}/contrib/macusers/macusers \
		${PREFIX}/bin/macusers
	[ -f ${PREFIX}/etc/afp.conf ] || \
		${INSTALL_DATA} -c ${PREFIX}/etc/afp.conf.dist ${PREFIX}/etc/afp.conf
	[ -f ${PREFIX}/etc/extmap.conf ] || \
		${INSTALL_DATA} -c ${PREFIX}/etc/extmap.conf.dist ${PREFIX}/etc/extmap.conf
	@${CAT} ${PKGMESSAGE}

.include <bsd.port.post.mk>
