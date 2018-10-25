from os.path import basename
import re

def clean(x):
  return re.sub(r'[:_+\.\/\\]', '-', x.lower()).replace('--', '-')

def extract(rule, path):
  name = clean('extract-' + rule + '-' + path)
  genrule(
    name = name,
    out = basename(path),
    cmd = 'cp $(location ' + rule + ')/' + path + ' $OUT',
  )
  return ':' + name

tools = glob([
  'Configure',
  'util/pod2mantest',
  'util/**/*.sh',
  'util/**/*.pl',
])

def configure(platform): 
  name = clean('configure-' + platform)
  genrule(
    name = name,
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
    cmd = ' && '.join([
      'cp -r $SRCDIR/. $TMP', 
      'mkdir -p $OUT', 
      'cd $TMP', 
      'chmod +x ' + ' '.join(tools), 
      './Configure shared ' + platform + ' --prefix=$OUT/build --openssldir=$OUT/build/openssl', 
      'cp -r $TMP/. $OUT', 
    ])
  )
  return ':' + name

def make(platform): 
  name = clean('make-' + platform)
  genrule(
    name = name,
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
    cmd = ' && '.join([
      'cp -r $SRCDIR/. $TMP', 
      'mkdir -p $OUT', 
      'cd $TMP', 
      'chmod +x ' + ' '.join(tools), 
      './Configure shared ' + platform + ' --prefix=$OUT/build --openssldir=$OUT/build/openssl', 
      'make -j4', 
      'make install', 
    ])
  )
  return ':' + name

linux_make = make('linux-x86_64')
macos_make = make('darwin64-x86_64-cc')
windows_make = make('VC-WIN64I')
ios_make = make('iphoneos-cross')

linux_configure = configure('linux-x86_64')
macos_configure = configure('darwin64-x86_64-cc')
windows_configure = configure('VC-WIN64I')
ios_configure = configure('iphoneos-cross')

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

extracted_headers = [
  'opensslconf.h',
]

def extract_header(rule, header):
  return extract(rule, 'include/openssl/' + header)

prebuilt_cxx_library(
  name = 'crypto',
  header_namespace = 'openssl',
  platform_shared_lib = [
    ('macos.*', extract(macos_make, 'build/lib/libcrypto.dylib')), 
    ('linux.*', extract(linux_make, 'build/lib/libcrypto.so')), 
    ('iphone.*', extract(ios_make, 'build/lib/libcrypto.dylib')), 
  ], 
  platform_static_lib = [
    ('macos.*', extract(macos_make, 'build/lib/libcrypto.a')), 
    ('linux.*', extract(linux_make, 'build/lib/libcrypto.a')), 
    ('iphone.*', extract(ios_make, 'build/lib/libcrypto.a')), 
  ], 
)

prebuilt_cxx_library(
  name = 'ssl',
  header_namespace = 'openssl',
  platform_shared_lib = [
    ('macos.*', extract(macos_make, 'build/lib/libssl.dylib')), 
    ('linux.*', extract(linux_make, 'build/lib/libssl.so')), 
    ('iphone.*', extract(ios_make, 'build/lib/libssl.dylib')), 
  ], 
  platform_static_lib = [
    ('macos.*', extract(macos_make, 'build/lib/libssl.a')), 
    ('linux.*', extract(linux_make, 'build/lib/libssl.a')), 
    ('iphone.*', extract(ios_make, 'build/lib/libssl.a')), 
  ], 
)

prebuilt_cxx_library(
  name = 'openssl',
  header_only = True,
  header_namespace = 'openssl',
  exported_platform_headers = [
    ('^macos.*', dict({ (x, extract_header(macos_configure, x)) for x in headers })),
    ('^linux.*', dict({ (x, extract_header(linux_configure, x)) for x in headers })),
    ('^iphone.*', dict({ (x, extract_header(ios_configure, x)) for x in headers })),
  ], 
  exported_deps = [
    ':crypto',
    ':ssl',
  ],
  visibility = [
    'PUBLIC',
  ],
)

cxx_binary(
  name = 'sha256', 
  srcs = [
    'sha256.cpp', 
  ],
  deps = [
    ':openssl', 
  ], 
)
