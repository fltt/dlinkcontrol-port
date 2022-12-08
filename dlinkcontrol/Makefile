PORTNAME=	dlinkcontrol
DISTVERSION=	1.0.1
CATEGORIES=	net-mgmt sysutils
DISTFILES=	gnulib-${GNULIB_GIT_COMMIT}${EXTRACT_SUFX}

MAINTAINER=	franz.lattanzio@gmail.com
COMMENT=	D-Link DWM-222 command-line utility
WWW=		https://github.com/fltt/dlinkcontrol/

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/COPYING

FETCH_DEPENDS=	git:devel/git

USES=		autoreconf

USE_GITHUB=	yes
GH_ACCOUNT=	fltt

GNU_CONFIGURE=	yes

PLIST_FILES=	${DOCSDIR_REL}/README.md \
		bin/dlinkcontrol

OPTIONS_DEFINE=		CURL
OPTIONS_DEFAULT=	CURL

CURL_LIB_DEPENDS=	libcurl.so:ftp/curl
CURL_CONFIGURE_WITH=	libcurl

GNULIB_GIT_URL=		git://git.sv.gnu.org/gnulib.git
GNULIB_GIT_COMMIT=	816e66d4315a7aa1d741bb1ebccb5578a1f8eada

pre-fetch:
	@if [ "${FORCE_FETCH_ALL}" = "true" ] || ! [ -f "${DISTDIR}/${DIST_SUBDIR}/gnulib-${GNULIB_GIT_COMMIT}${EXTRACT_SUFX}" ]; then \
	  ${MKDIR} "${DISTDIR}/${DIST_SUBDIR}" && \
	  cd "${DISTDIR}/${DIST_SUBDIR}" && \
	  git clone -n "${GNULIB_GIT_URL}" gnulib-${GNULIB_GIT_COMMIT} && \
	  (cd gnulib-${GNULIB_GIT_COMMIT} && \
	   git checkout -q ${GNULIB_GIT_COMMIT} && \
	   ${RM} -r .git) && \
	  ${FIND} gnulib-${GNULIB_GIT_COMMIT} -and -exec ${TOUCH} -h -d 1970-01-01T00:00:00Z {} \; && \
	  ${FIND} gnulib-${GNULIB_GIT_COMMIT} -print0 | LC_ALL=C ${SORT} -z | \
	    ${TAR} czf gnulib-${GNULIB_GIT_COMMIT}${EXTRACT_SUFX} --format=bsdtar --gid 0 --uid 0 --options gzip:!timestamp --no-recursion --null -T - && \
	  ${RM} -r gnulib-${GNULIB_GIT_COMMIT}; \
	fi

pre-configure:
	@cd ${WRKSRC} && \
		"${WRKDIR}/gnulib-${GNULIB_GIT_COMMIT}/gnulib-tool" --update

.include <bsd.port.mk>
