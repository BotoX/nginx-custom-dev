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
_fancyindex_commit="" # https://github.com/aperezdc/ngx-fancyindex
_cachepurge_tag="2.3" # https://github.com/FRiCKLE/ngx_cache_purge
_slowfscache_tag="1.10" # https://github.com/FRiCKLE/ngx_slowfs_cache
_uploadprogress_tag="v0.9.2" # https://github.com/masterzen/nginx-upload-progress-module
_headersmore_tag="v0.33" # https://github.com/openresty/headers-more-nginx-module
_echo_tag="v0.61" # https://github.com/openresty/echo-nginx-module
_upstreamfair_commit="6cb41999758c9299fa9d6b9a6d9fdfd8cc133dc1" # https://github.com/ximik777/nginx-upstream-fair
_authpam_tag="v1.5.1" # https://github.com/sto/ngx_http_auth_pam_module
_pagespeed_version="1.13.35.2" # https://github.com/pagespeed/ngx_pagespeed
_rtmp_branch="dev" # https://github.com/sergey-dryabzhinsky/nginx-rtmp-module
_davext_tag="v3.0.0" # https://github.com/arut/nginx-dav-ext-module
_naxsi_tag="0.56" # https://github.com/nbs-system/naxsi
_substitutions_tag="v0.6.4" # https://github.com/yaoweibin/ngx_http_substitutions_filter_module
_lua_tag="v0.10.14rc3" # https://github.com/openresty/lua-nginx-module
_brotli_commit="bfd2885b2da4d763fed18f49216bb935223cd34b" # https://github.com/google/ngx_brotli
_vts_tag="v0.1.18" # https://github.com/vozlt/nginx-module-vts
_mtask_commit="828df3c72755f10811473a5d0b049b04a153fe63" # https://github.com/arut/nginx-mtask-module
_mysql_commit="f97cf60a1b776558f6f33fb7b1b8facf1b1f381d" # https://github.com/ideal/nginx-mysql-module

pkgname=nginx-custom-dev
pkgver=1.14.2
pkgrel=1
pkgdesc="Development version of lightweight HTTP server and IMAP/POP3 proxy server with standard, additional and 3d party modules"
arch=('i686' 'x86_64')

depends=('pcre' 'zlib' 'openssl' 'pam' 'geoip' 'geoip-database' 'gd' 'libxslt' 'luajit' 'brotli' 'libmariadbclient')
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
    "nginx-mysql-module.diff"
    "ngx-fancyindex::git+https://github.com/aperezdc/ngx-fancyindex#commit=${_fancyindex_commit}"
    "ngx_cache_purge::git+https://github.com/FRiCKLE/ngx_cache_purge.git#tag=${_cachepurge_tag}"
    "ngx_slowfs_cache::git+https://github.com/FRiCKLE/ngx_slowfs_cache.git#tag=${_slowfscache_tag}"
    "nginx-upload-progress-module::git+https://github.com/masterzen/nginx-upload-progress-module#tag=${_uploadprogress_tag}"
    "headers-more-nginx-module::git+https://github.com/openresty/headers-more-nginx-module#tag=${_headersmore_tag}"
    "echo-nginx-module::git+https://github.com/openresty/echo-nginx-module#tag=${_echo_tag}"
    "nginx-upstream-fair::git+https://github.com/ximik777/nginx-upstream-fair#commit=${_upstreamfair_commit}"
    "ngx_http_auth_pam_module::git+https://github.com/stogh/ngx_http_auth_pam_module#tag=${_authpam_tag}"
    "ngx_pagespeed::git+https://github.com/pagespeed/ngx_pagespeed#tag=v${_pagespeed_version}-stable"
    "psol.tar.gz::https://dl.google.com/dl/page-speed/psol/${_pagespeed_version}-x64.tar.gz"
    "nginx-rtmp-module::git+https://github.com/sergey-dryabzhinsky/nginx-rtmp-module#branch=${_rtmp_branch}"
    "nginx-dav-ext-module::git+https://github.com/arut/nginx-dav-ext-module#tag=${_davext_tag}"
    "naxsi::git+https://github.com/nbs-system/naxsi#tag=${_naxsi_tag}"
    "ngx_http_substitutions_filter_module::git+https://github.com/yaoweibin/ngx_http_substitutions_filter_module#tag=${_substitutions_tag}"
    "lua-nginx-module::git+https://github.com/openresty/lua-nginx-module#tag=${_lua_tag}"
    "ngx_brotli::git+https://github.com/google/ngx_brotli#commit=${_brotli_commit}"
    "brotli::git+https://github.com/google/brotli"
    "nginx-module-vts::git+https://github.com/vozlt/nginx-module-vts#tag=${_vts_tag}"
    "nginx-mtask-module::git+https://github.com/arut/nginx-mtask-module#commit=${_mtask_commit}"
    "nginx-mysql-module::git+https://github.com/ideal/nginx-mysql-module#commit=${_mysql_commit}"
)

md5sums=('d56559ed5e8cc0b1c7adbe33f2300c4c'
         '845cab784b50f1666bbf89d7435ac7af'
         '79031b58828462dec53a9faed9ddb36a'
         '6696dc228a567506bca3096b5197c9db'
         '239b829a13cea1d244c1044e830bd9c2'
         '839645bb987bcffc02162b14d8eea0e2'
         'd7bdc78a212438e553b156f6fd61f750'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         '40de2a0f70fd9c1a794832e6b553fce3'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP'
         'SKIP')

prepare() {
  if [ ! -d "$srcdir/ngx_pagespeed/psol" ]; then
    mv "$srcdir/psol" "$srcdir/ngx_pagespeed/"
  fi

  cd ngx_brotli
  git submodule init
  git config submodule."deps/brotli".url "$srcdir/brotli"
  git submodule update

  cd "$srcdir/ngx-fancyindex"
  git apply --ignore-space-change --ignore-whitespace \
    "$srcdir/ngx-fancyindex.diff"

  cd "$srcdir/nginx-mysql-module"
  git apply --ignore-space-change --ignore-whitespace \
    "$srcdir/nginx-mysql-module.diff"
}

build() {
  local _src_dir="${srcdir}/${_pkgname}-${pkgver}"

  cd $_src_dir

  export LUAJIT_LIB=/usr/lib/
  export LUAJIT_INC=/usr/include/luajit-2.0/

  echo y | ./configure \
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
    --add-module="../lua-nginx-module" \
    --add-module="../ngx_brotli" \
    --add-module="../nginx-module-vts" \
    --add-module="../nginx-mtask-module" \
    --add-module="../nginx-mysql-module"

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
