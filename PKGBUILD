# Maintainer: Alexander Kuznecov <alexander@kuznetcov.me>

_pkgname="nginx"
_user="http"
_group="http"
_doc_root="/usr/share/${_pkgname}/html"
_sysconf_path="etc"
_conf_path="${_sysconf_path}/${_pkgname}"
_tmp_path="/var/spool/${_pkgname}"
_pid_path="/run"
_lock_path="/var/lock"
_log_path="/var/log/${_pkgname}"

### 3d party modules:
_fancyindex_tag="v0.3.5"
_cachepurge_tag="2.3"
_slowfscache_tag="1.10"
_uploadprogress_tag="v0.9.1"
_headersmore_tag="v0.29"
_echo_tag="v0.58"
_upstreamfair_commit="a18b4099fbd458111983200e098b6f0c8efed4bc"
_authpam_tag="v1.4"
_pagespeed_version="1.9.32.10"
_davext_tag="v0.0.3"
_naxsi_tag="0.54"
_substitutions_tag="v0.6.4"
_lua_tag="v0.10.0"

pkgname=nginx-custom-dev
pkgver=1.9.10
pkgrel=1
pkgdesc="Development version of lightweight HTTP server and IMAP/POP3 proxy server with standard, additional and 3d party modules"
arch=('i686' 'x86_64')

depends=('pcre' 'zlib' 'openssl' 'pam' 'geoip' 'geoip-database' 'gd' 'libxslt' 'luajit')
makedepends=('libxslt' 'gd' 'git')

url="http://nginx.org"
license=('custom')
conflicts=('nginx' 'nginx-unstable' 'nginx-svn' 'nginx-devel' 'nginx-custom' 'nginx-full')
provides=('nginx')
backup=("${_conf_path}/nginx.conf"
  "${_conf_path}/koi-win"
  "${_conf_path}/koi-utf"
  "${_conf_path}/win-utf"
  "${_conf_path}/mime.types"
  "${_conf_path}/fastcgi.conf"
  "${_conf_path}/fastcgi_params"
  "${_conf_path}/scgi_params"
  "${_conf_path}/uwsgi_params"
  "etc/logrotate.d/nginx")
_user=http
_group=http

source=("nginx.sh"
    "nginx.conf"
    "nginx.logrotate"
    "nginx.service"
    "http://nginx.org/download/nginx-$pkgver.tar.gz"
    "ngx-fancyindex.diff"
    "ngx_pagespeed.diff"
    "ngx-fancyindex::git+https://github.com/aperezdc/ngx-fancyindex#tag=${_fancyindex_tag}"
    "ngx_cache_purge::git+https://github.com/FRiCKLE/ngx_cache_purge.git#tag=${_cachepurge_tag}"
    "ngx_slowfs_cache::git+https://github.com/FRiCKLE/ngx_slowfs_cache.git#tag=${_slowfscache_tag}"
    "nginx-upload-progress-module::git+https://github.com/masterzen/nginx-upload-progress-module#tag=${_uploadprogress_tag}"
    "headers-more-nginx-module::git+https://github.com/agentzh/headers-more-nginx-module#tag=${_headersmore_tag}"
    "echo-nginx-module::git+https://github.com/agentzh/echo-nginx-module#tag=${_echo_tag}"
    "nginx-upstream-fair::git+https://github.com/gnosek/nginx-upstream-fair#commit=${_upstreamfair_commit}"
    "ngx_http_auth_pam_module::git+https://github.com/stogh/ngx_http_auth_pam_module#tag=${_authpam_tag}"
    "ngx_pagespeed::git+https://github.com/pagespeed/ngx_pagespeed#tag=v${_pagespeed_version}-beta"
    "psol.tar.gz::https://dl.google.com/dl/page-speed/psol/${_pagespeed_version}.tar.gz"
    "nginx-rtmp-module::git+https://github.com/arut/nginx-rtmp-module#tag=${_rtmp_tag}"
    "nginx-dav-ext-module::git+https://github.com/arut/nginx-dav-ext-module#tag=${_davext_tag}"
    "naxsi::git+https://github.com/nbs-system/naxsi#tag=${_naxsi_tag}"
    "ngx_http_substitutions_filter_module::git+https://github.com/yaoweibin/ngx_http_substitutions_filter_module#tag=${_substitutions_tag}"
    "lua-nginx-module::git+https://github.com/chaoslawful/lua-nginx-module#tag=${_lua_tag}"
)

md5sums=('d56559ed5e8cc0b1c7adbe33f2300c4c'
         '845cab784b50f1666bbf89d7435ac7af'
         '79031b58828462dec53a9faed9ddb36a'
         '6696dc228a567506bca3096b5197c9db'
         '64cc970988356a5e0fc4fcd1ab84fe57'
         '47adc600c72cfb59754eff3b7850a6f3'
         '528a86490f918d0a5d09bc12cda2b365'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'c4069b751887d736f643ba698239c514'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP')

prepare() {
  if [ ! -d "$srcdir/ngx_pagespeed/psol" ]; then
    mv "$srcdir/psol" "$srcdir/ngx_pagespeed/"
  fi

  cd "$srcdir/ngx-fancyindex"
  git apply --ignore-space-change --ignore-whitespace \
    "$srcdir/ngx-fancyindex.diff"

  cd "$srcdir/ngx_pagespeed"
  git apply --ignore-space-change --ignore-whitespace \
    "$srcdir/ngx_pagespeed.diff"
}

build() {
  local _src_dir="${srcdir}/${_pkgname}-${pkgver}"

  cd $_src_dir

  export LUAJIT_LIB=/usr/lib/
  export LUAJIT_INC=/usr/include/luajit-2.0/

  ./configure \
    --prefix="/${_conf_path}" \
    --conf-path="/${_conf_path}/nginx.conf" \
    --sbin-path="/usr/bin/${_pkgname}" \
    --pid-path="${_pid_path}/${_pkgname}.pid" \
    --lock-path=${_pid_path}/${_pkgname}.lock \
    --http-client-body-temp-path=${_tmp_path}/client_body_temp \
    --http-proxy-temp-path=${_tmp_path}/proxy_temp \
    --http-fastcgi-temp-path=${_tmp_path}/fastcgi_temp \
    --http-uwsgi-temp-path=${_tmp_path}/uwsgi_temp \
    --http-scgi-temp-path=${_tmp_path}scgi_temp \
    --http-log-path=${_log_path}/access.log \
    --error-log-path=${_log_path}/error.log \
    --user=${_user} \
    --group=${_group} \
    --with-debug \
    --with-ipv6 \
    --with-mail \
    --add-module="../naxsi/naxsi_src" \
    --with-mail_ssl_module \
    --with-http_ssl_module \
    --with-http_stub_status_module \
    --with-http_dav_module \
    --with-http_gzip_static_module \
    --with-http_realip_module \
    --with-http_addition_module \
    --with-http_xslt_module \
    --with-http_image_filter_module \
    --with-http_sub_module \
    --with-http_flv_module \
    --with-http_mp4_module \
    --with-http_random_index_module \
    --with-http_secure_link_module \
    --with-http_perl_module \
    --with-http_degradation_module \
    --with-http_geoip_module \
    --with-http_v2_module \
    --with-http_gunzip_module \
    --with-http_auth_request_module \
    --add-module="../ngx-fancyindex" \
    --add-module="../ngx_cache_purge" \
    --add-module="../ngx_slowfs_cache" \
    --add-module="../nginx-upload-progress-module" \
    --add-module="../headers-more-nginx-module" \
    --add-module="../echo-nginx-module" \
    --add-module="../nginx-upstream-fair" \
    --add-module="../ngx_http_auth_pam_module" \
    --add-module="../ngx_pagespeed" \
    --add-module="../nginx-rtmp-module" \
    --add-module="../nginx-dav-ext-module" \
    --add-module="../ngx_http_substitutions_filter_module" \
    --add-module="../lua-nginx-module"

  make
}

package() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  make DESTDIR="$pkgdir/" install

  sed -e "s|\<user\s\+\w\+;|user $_user $_group;|g" \
    -e '44s|html|/usr/share/nginx/html|' \
    -e '54s|html|/usr/share/nginx/html|' \
    -i ${pkgdir}/$_conf_path/nginx.conf

  install -d "${pkgdir}/${_tmp_path}"
  install -d "${pkgdir}/${_doc_root}"

  mv "${pkgdir}/${_conf_path}/html/"* "${pkgdir}/${_doc_root}"
  rm -rf "${pkgdir}/${_conf_path}/html"

  install -D -m555 "${srcdir}/nginx.sh" "${pkgdir}/etc/rc.d/${_pkgname}"
  install -D -m644 "${srcdir}/nginx.logrotate" "${pkgdir}/etc/logrotate.d/${_pkgname}"
  install -D -m644 "${srcdir}/nginx.conf" "${pkgdir}/etc/conf.d/${_pkgname}"
  install -D -m644 "${srcdir}/nginx.service" "${pkgdir}/usr/lib/systemd/system/nginx.service"
  install -D -m644 "LICENSE" "${pkgdir}/usr/share/licenses/${_pkgname}/LICENSE"
  install -D -m644 "man/nginx.8" "${pkgdir}/usr/share/man/man8/nginx.8"
}
