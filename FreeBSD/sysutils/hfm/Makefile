# $FreeBSD$

PORTNAME=	hfm
PORTVERSION=	1.1.2
DISTVERSIONPREFIX=	v
CATEGORIES=	sysutils

MAINTAINER=	554b8425@razorfever.net
COMMENT=	Run tests in parallel at high frequency

LICENSE=	BSD2CLAUSE

# gb 0.4 includes FreeBSD-specific fixes that this port requires
#   https://github.com/constabulary/gb/issues/506
BUILD_DEPENDS=	gb>=0.4:${PORTSDIR}/devel/gb \
		git:${PORTSDIR}/devel/git-lite \
		${LOCALBASE}/lib/libucl.a:${PORTSDIR}/textproc/libucl

USE_GITHUB=	yes
GH_ACCOUNT=	derekmarcotte

MAKE_ARGS+=	ETCDIR=${ETCDIR} TAG=${DISTVERSIONPREFIX}${PORTVERSION}

NO_INSTALL=	yes
ALL_TARGET=	test build

pre-patch:
	(cd ${WRKSRC}; make patch-local-go-libucl)

do-install:
	@${MKDIR} ${STAGEDIR}${PREFIX}/bin
	${INSTALL_PROGRAM} ${WRKSRC}/bin/hfm ${STAGEDIR}${PREFIX}/bin
	@${MKDIR} ${STAGEDIR}${ETCDIR}
	${INSTALL_DATA} ${WRKSRC}/examples/hfm.conf.sample ${STAGEDIR}${ETCDIR}
	@${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/examples/* ${STAGEDIR}${EXAMPLESDIR}
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/README.md ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/doc/* ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
