# $FreeBSD$

NO_MAN=

.include <bsd.own.mk>

.PATH: ${.CURDIR}/../../../contrib/ntp/ntpdc

PROG=	ntpdc
SRCS= 	ntpdc.c ntpdc_ops.c ntpdc-opts.c version.c

CFLAGS+= -I${.CURDIR}/../../../contrib/ntp/include \
	-I${.CURDIR}/../../../contrib/ntp/lib/isc/include \
	-I${.CURDIR}/../../../contrib/ntp/lib/isc/unix/include \
	-I${.CURDIR}/../../../contrib/ntp/lib/isc/pthreads/include \
	-I${.CURDIR}/../../../contrib/ntp/sntp/libopts \
	-I${.CURDIR}/../../../lib/libc/${MACHINE_ARCH} \
	-I${.CURDIR}/../ -I${.CURDIR}

DPADD=	${LIBNTP} ${LIBM} ${LIBOPTS} ${LIBEDIT} ${LIBTERMCAP} ${LIBPTHREAD}
LDADD=	${LIBNTP} -lm ${LIBOPTS} -ledit -ltermcap -lpthread

CFLAGS+=	-DHAVE_LIBEDIT -DHAVE_READLINE_READLINE_H \
		-I${DESTDIR}/${INCLUDEDIR}/edit

.if ${MK_OPENSSL} != "no"
DPADD+=	${LIBCRYPTO}
LDADD+=	-lcrypto
.else
DPADD+=	${LIBMD}
LDADD+=	-lmd
.endif

CLEANFILES+= .version version.c

version.c:
	sh -e ${.CURDIR}/../scripts/mkver ntpdc

afterinstall:
	rm -f ${DESTDIR}/usr/sbin/xntpdc

.include <bsd.prog.mk>
