tools = glob([
  'Configure',
  'util/pod2mantest',
  'util/**/*.sh',
  'util/**/*.pl',
])

genrule(
  name = 'make',
  out = 'out',
  srcs = glob([
    'apps/**/*',
    'apps/**/*.h',
    'apps/**/*.c',
    'apps/**/*.cnf',
    'apps/**/*.srl',
    'apps/**/*.pl',
    'apps/**/*.pem',
    'apps/**/*.in',
    'apps/**/*.sh',
    'apps/**/*.txt',
    'apps/**/*.attr',
    'apps/**/Makefile',
    'certs/**/*.crl',
    'certs/**/*.pem',
    'crypto/**/*.h',
    'crypto/**/*.c',
    'crypto/**/*.cnf',
    'crypto/**/*.in',
    'crypto/**/*.inl',
    'crypto/**/*.pl',
    'crypto/**/*.num',
    'crypto/**/*.txt',
    'crypto/**/Makefile',
    'doc/**/*.el',
    'doc/**/*.pod',
    'doc/**/*.txt',
    'engines/**/*.h',
    'engines/**/*.c',
    'engines/**/*.bat',
    'engines/**/*.opt',
    'engines/**/*.mar',
    'engines/**/*.proto',
    'engines/**/*.ec',
    'engines/**/Makefile',
    'ssl/**/*.h',
    'ssl/**/*.c',
    'ssl/**/*.inl',
    'ssl/**/*.pl',
    'ssl/**/Makefile',
    'test/**/*.h',
    'test/**/*.c',
    'test/**/*.inl',
    'test/**/*.pl',
    'test/**/Makefile',
    'tools/**/*',
    'util/**/*',
    '*.h',
    'config',
    'Configure',
    'FAQ',
    'INSTALL',
    'INSTALL.*',
    'LICENSE',
    'Makefile.*',
    'TABLE',
  ]),
  cmd = 'platform=\$(case $(uname) in ' +
    '("Linux") ' +
    '  echo "linux-x86_64" ' +
    ';; ' +
    '("Darwin") ' +
    '  echo "darwin64-x86_64-cc" ' +
    ';; ' +
    '(*) ' +
    '  echo "Unknown" ' +
    ';; ' +
  'esac); ' +
  'cp -r $SRCDIR/. $TMP && ' + 
  'mkdir -p $OUT && ' + 
  'cd $TMP && ' +
  'chmod +x ' + ' '.join(tools) + ' && ' +
  './Configure shared $platform --prefix=$OUT/build --openssldir=$OUT/build/openssl && ' +
  'make -j4 && ' + 
  'make install'
)

headers = [
  'aes.h',
  'asn1.h',
  'asn1_mac.h',
  'asn1t.h',
  'bio.h',
  'blowfish.h',
  'bn.h',
  'buffer.h',
  'camellia.h',
  'cast.h',
  'cmac.h',
  'cms.h',
  'comp.h',
  'conf.h',
  'conf_api.h',
  'crypto.h',
  'des.h',
  'des_old.h',
  'dh.h',
  'dsa.h',
  'dso.h',
  'dtls1.h',
  'e_os2.h',
  'ebcdic.h',
  'ec.h',
  'ecdh.h',
  'ecdsa.h',
  'engine.h',
  'err.h',
  'evp.h',
  'hmac.h',
  'idea.h',
  'krb5_asn.h',
  'kssl.h',
  'lhash.h',
  'md4.h',
  'md5.h',
  'mdc2.h',
  'modes.h',
  'obj_mac.h',
  'objects.h',
  'ocsp.h',
  'opensslconf.h',
  'opensslv.h',
  'ossl_typ.h',
  'pem.h',
  'pem2.h',
  'pkcs12.h',
  'pkcs7.h',
  'pqueue.h',
  'rand.h',
  'rc2.h',
  'rc4.h',
  'ripemd.h',
  'rsa.h',
  'safestack.h',
  'seed.h',
  'sha.h',
  'srp.h',
  'srtp.h',
  'ssl.h',
  'ssl2.h',
  'ssl23.h',
  'ssl3.h',
  'stack.h',
  'symhacks.h',
  'tls1.h',
  'ts.h',
  'txt_db.h',
  'ui.h',
  'ui_compat.h',
  'whrlpool.h',
  'x509.h',
  'x509_vfy.h',
  'x509v3.h',
]

def extract(x):
  genrule(
    name = x,
    out = x,
    cmd = 'cp $(location :make)/build/include/openssl/' + x + ' $OUT',
  )
  return ':' + x

genrule(
  name = 'crypto-shared-macos', 
  out = 'libcrypto.dylib', 
  cmd = 'cp $(location :make)/build/lib/libcrypto.dylib', 
)

genrule(
  name = 'crypto-static-macos', 
  out = 'libcrypto.a', 
  cmd = 'cp $(location :make)/build/lib/libcrypto.a', 
)

genrule(
  name = 'crypto-shared-linux', 
  out = 'libcrypto.so', 
  cmd = 'cp $(location :make)/build/lib/libcrypto.so', 
)

genrule(
  name = 'crypto-static-linux', 
  out = 'libcrypto.a', 
  cmd = 'cp $(location :make)/build/lib/libcrypto.a', 
)

genrule(
  name = 'ssl-shared-macos', 
  out = 'libssl.dylib', 
  cmd = 'cp $(location :make)/build/lib/libssl.dylib', 
)

genrule(
  name = 'ssl-static-macos', 
  out = 'libssl.a', 
  cmd = 'cp $(location :make)/build/lib/libssl.a', 
)

genrule(
  name = 'ssl-shared-linux', 
  out = 'libssl.so', 
  cmd = 'cp $(location :make)/build/lib/libssl.so', 
)

genrule(
  name = 'ssl-static-linux', 
  out = 'libssl.a', 
  cmd = 'cp $(location :make)/build/lib/libssl.a', 
)

prebuilt_cxx_library(
  name = 'crypto',
  header_namespace = 'openssl',
  platform_shared_lib = [
    ('^macos.*', ':crypto-shared-macos'), 
    ('^linux.*', ':crypto-shared-linux'), 
  ], 
  platform_static_lib = [
    ('^macos.*', ':crypto-static-macos'), 
    ('^linux.*', ':crypto-static-linux'), 
  ], 
)

prebuilt_cxx_library(
  name = 'ssl',
  header_namespace = 'openssl',
  platform_shared_lib = [
    ('^macos.*', ':ssl-shared-macos'), 
    ('^linux.*', ':ssl-shared-linux'), 
  ], 
  platform_static_lib = [
    ('^macos.*', ':ssl-static-macos'), 
    ('^linux.*', ':ssl-static-linux'), 
  ], 
)

prebuilt_cxx_library(
  name = 'openssl',
  header_only = True,
  header_namespace = 'openssl',
  exported_headers = dict({ (x, extract(x)) for x in headers }),
  exported_deps = [
    ':crypto',
    ':ssl',
  ],
  visibility = [
    'PUBLIC',
  ],
)
