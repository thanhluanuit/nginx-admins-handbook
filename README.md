<div align="center">
  <h1>Nginx Admin's Handbook</h1>
</div>

<div align="center">
  <b><code>My notes on NGINX administration basics, tips & tricks, caveats, and gotchas.</code></b>
</div>

<br>

<p align="center">
  <a href="https://www.hostingadvice.com/how-to/nginx-vs-apache/">
    <img src="https://github.com/trimstray/nginx-admins-handbook/blob/master/static/img/nginx_meme.png" alt="Meme">
  </a>
</p>

<br>

<p align="center">
  <sup>
    <i>
      Hi-diddle-diddle, he played on his<br>
      fiddle and danced with lady pigs.<br>
      Number three said, "Nicks on tricks!<br>
      I'll build my house with <b>EN-jin-EKS</b>!".<br>
      <a href="https://g.co/kgs/HCcQVz">The Three Little Pigs: Who's Afraid of the Big Bad Wolf?</a>
    </i>
  </sup>
</p>

<br>

<p align="center">
  <a href="https://github.com/trimstray/nginx-admins-handbook/pulls">
    <img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg?longCache=true" alt="Pull Requests">
  </a>
  <a href="http://www.gnu.org/licenses/">
    <img src="https://img.shields.io/badge/License-GNU-blue.svg?longCache=true" alt="License">
  </a>
</p>

<div align="center">
  <sub>Created by
  <a href="https://twitter.com/trimstray">trimstray</a> and
  <a href="https://github.com/trimstray/nginx-admins-handbook/graphs/contributors">contributors</a>
</div>

<br>

****

# Table of Contents

- **[Introduction](#introduction)**<a id="toc-introduction"></a>
  * [Prologue](#prologue)
  * [Why I Created This Handbook](#why-i-created-this-handbook)
  * [Who This Handbook is For](#who-this-handbook-is-for)
  * [Before You Start](#before-you-start)
  * [Contributing & Support](#contributing--support)
  * [Checklist to rule them all](#checklist-to-rule-them-all)
- **[Bonus Stuff](#bonus-stuff)**<a id="toc-bonus-stuff"></a>
  * [Reports: blkcipher.info](#reports-blkcipherinfo)
    * [SSL Labs](#ssl-labs)
    * [Mozilla Observatory](#mozilla-observatory)
  * [Printable hardening cheatsheets](#printable-hardening-cheatsheets)
  * [Fully automatic installation](#fully-automatic-installation)
  * [Static error pages generator](#static-error-pages-generator)
- **[Books](#books)**<a id="toc-books"></a>
  * [Nginx Essentials](#nginx-essentials)
  * [Nginx Cookbook](#nginx-cookbook)
  * [Nginx HTTP Server](#nginx-http-server)
  * [Nginx High Performance](#nginx-high-performance)
  * [Mastering Nginx](#mastering-nginx)
  * [ModSecurity 3.0 and NGINX: Quick Start Guide](#modsecurity-30-and-nginx-quick-start-guide)
  * [Cisco ACE to NGINX: Migration Guide](#cisco-ace-to-nginx-migration-guide)
- **[External Resources](#external-resources)**<a id="toc-external-resources"></a>
  * [Nginx official](#nginx-official)
  * [Nginx distributions](#nginx-distributions)
  * [Comparison reviews](#comparison-reviews)
  * [Cheatsheets & References](#cheatsheets--references)
  * [Performance & Hardening](#performance--hardening)
  * [Presentations & Videos](#presentations--videos)
  * [Playgrounds](#playgrounds)
  * [Config generators](#config-generators)
  * [Static analyzers](#static-analyzers)
  * [Log analyzers](#log-analyzers)
  * [Performance analyzers](#performance-analyzers)
  * [Builder tools](#builder-tools)
  * [Benchmarking tools](#benchmarking-tools)
  * [Debugging tools](#debugging-tools)
  * [Development](#development)
  * [Online tools](#online-tools)
  * [Other stuff](#other-stuff)
- **[What's next?](#whats-next)**

<details>
<summary><b>Other chapters</b></summary><br>

- **[HTTP Basics](doc/HTTP_BASICS.md#http-basics)**<a id="toc-http-basics"></a>
  * [Features and architecture](doc/HTTP_BASICS.md#features-and-architecture)
  * [URI vs URL](doc/HTTP_BASICS.md#uri-vs-url)
  * [HTTP Headers](doc/HTTP_BASICS.md#http-headers)
  * [HTTP Methods](doc/HTTP_BASICS.md#http-methods)
  * [Request](doc/HTTP_BASICS.md#request)
    * [Request line](doc/HTTP_BASICS.md#request-line)
      * [Methods](doc/HTTP_BASICS.md#methods)
      * [Request URI](doc/HTTP_BASICS.md#request-uri)
      * [HTTP version](doc/HTTP_BASICS.md#http-version)
    * [Request header fields](doc/HTTP_BASICS.md#request-header-fields)
    * [Message body](doc/HTTP_BASICS.md#message-body)
    * [Generate requests](doc/HTTP_BASICS.md#generate-requests)
  * [Response](doc/HTTP_BASICS.md#response)
    * [Status line](doc/HTTP_BASICS.md#status-line)
      * [HTTP version](doc/HTTP_BASICS.md#http-version-1)
      * [Status codes and reason phrase](doc/HTTP_BASICS.md#status-codes-and-reason-phrase)
    * [Response header fields](doc/HTTP_BASICS.md#response-header-fields)
    * [Message body](doc/HTTP_BASICS.md#message-body-1)
- **[SSL/TLS Basics](doc/SSL_TLS_BASICS.md#ssltls-basics)**<a id="toc-ssltls-basics"></a>
  * [TLS versions](doc/SSL_TLS_BASICS.md#tls-versions)
  * [TLS handshake](doc/SSL_TLS_BASICS.md#tls-handshake)
  * [Cipher suites](doc/SSL_TLS_BASICS.md#cipher-suites)
  * [Diffie-Hellman key exchange](doc/SSL_TLS_BASICS.md#diffie-hellman-key-exchange)
- **[NGINX Basics](doc/NGINX_BASICS.md#nginx-basics)**<a id="toc-nginx-basics"></a>
  * [Directories and files](doc/NGINX_BASICS.md#directories-and-files)
  * [Commands](doc/NGINX_BASICS.md#commands)
  * [Processes](doc/NGINX_BASICS.md#processes)
  * [Configuration syntax](doc/NGINX_BASICS.md#configuration-syntax)
    * [Comments](doc/NGINX_BASICS.md#comments)
    * [End of lines](doc/NGINX_BASICS.md#end-of-lines)
    * [Variables, Strings, and Quotes](doc/NGINX_BASICS.md#variables-strings-and-quotes)
    * [Directives, Blocks, and Contexts](doc/NGINX_BASICS.md#directives-blocks-and-contexts)
    * [External files](doc/NGINX_BASICS.md#external-files)
    * [Measurement units](doc/NGINX_BASICS.md#measurement-units)
    * [Regular expressions with PCRE](doc/NGINX_BASICS.md#regular-expressions-with-pcre)
    * [Enable syntax highlighting](doc/NGINX_BASICS.md#enable-syntax-highlighting)
  * [Connection processing](doc/NGINX_BASICS.md#connection-processing)
    * [Event-Driven architecture](doc/NGINX_BASICS.md#event-driven-architecture)
    * [Multiple processes](doc/NGINX_BASICS.md#multiple-processes)
    * [Simultaneous connections](doc/NGINX_BASICS.md#simultaneous-connections)
    * [HTTP Keep-Alive connections](doc/NGINX_BASICS.md#http-keep-alive-connections)
  * [Request processing stages](doc/NGINX_BASICS.md#request-processing-stages)
  * [Server blocks logic](doc/NGINX_BASICS.md#server-blocks-logic)
    * [Handle incoming connections](doc/NGINX_BASICS.md#handle-incoming-connections)
    * [Matching location](doc/NGINX_BASICS.md#matching-location)
    * [rewrite vs return](doc/NGINX_BASICS.md#rewrite-vs-return)
    * [try_files directive](doc/NGINX_BASICS.md#try_files-directive)
    * [if, break, and set](doc/NGINX_BASICS.md#if-break-and-set)
    * [root vs alias](doc/NGINX_BASICS.md#root-vs-alias)
    * [internal directive](doc/NGINX_BASICS.md#internal-directive)
    * [External and internal redirects](doc/NGINX_BASICS.md#external-and-internal-redirects)
  * [Log files](doc/NGINX_BASICS.md#log-files)
    * [Conditional logging](doc/NGINX_BASICS.md#conditional-logging)
    * [Manually log rotation](doc/NGINX_BASICS.md#manually-log-rotation)
    * [Error log severity levels](doc/NGINX_BASICS.md#error-log-severity-levels)
  * [Reverse proxy](doc/NGINX_BASICS.md#reverse-proxy)
    * [Passing requests](doc/NGINX_BASICS.md#passing-requests)
    * [Trailing slashes](doc/NGINX_BASICS.md#trailing-slashes)
    * [Processing headers](doc/NGINX_BASICS.md#processing-headers)
    * [Passing headers](doc/NGINX_BASICS.md#passing-headers)
      * [Importance of the Host header](doc/NGINX_BASICS.md#importance-of-the-host-header)
      * [Redirects and X-Forwarded-Proto](doc/NGINX_BASICS.md#redirects-and-x-forwarded-proto)
      * [A warning about the X-Forwarded-For](doc/NGINX_BASICS.md#a-warning-about-the-x-forwarded-for)
      * [Improve extensibility with Forwarded](doc/NGINX_BASICS.md#improve-extensibility-with-forwarded)
  * [Load balancing algorithms](doc/NGINX_BASICS.md#load-balancing-algorithms)
    * [Backend parameters](doc/NGINX_BASICS.md#backend-parameters)
    * [Upstream servers with SSL](doc/NGINX_BASICS.md#upstream-servers-with-ssl)
    * [Round Robin](doc/NGINX_BASICS.md#round-robin)
    * [Weighted Round Robin](doc/NGINX_BASICS.md#weighted-round-robin)
    * [Least Connections](doc/NGINX_BASICS.md#least-connections)
    * [Weighted Least Connections](doc/NGINX_BASICS.md#weighted-least-connections)
    * [IP Hash](doc/NGINX_BASICS.md#ip-hash)
    * [Generic Hash](doc/NGINX_BASICS.md#generic-hash)
    * [Other methods](doc/NGINX_BASICS.md#other-methods)
  * [Rate limiting](doc/NGINX_BASICS.md#rate-limiting)
    * [Variables](doc/NGINX_BASICS.md#variables)
    * [Directives, keys, and zones](doc/NGINX_BASICS.md#directives-keys-and-zones)
    * [Burst and nodelay parameters](doc/NGINX_BASICS.md#burst-and-nodelay-parameters)
  * [3rd party modules](doc/NGINX_BASICS.md#3rd-party-modules)
    * [ngx_set_misc](doc/NGINX_BASICS.md#ngx_set_misc)
    * [ngx_http_geoip_module](doc/NGINX_BASICS.md#ngx_http_geoip_module)
- **[Helpers](doc/HELPERS.md#helpers)**<a id="toc-helpers"></a>
  * [Installing from prebuilt packages](doc/HELPERS.md#installing-from-prebuilt-packages)
    * [RHEL7 or CentOS 7](doc/HELPERS.md#rhel7-or-centos-7)
    * [Debian or Ubuntu](doc/HELPERS.md#debian-or-ubuntu)
    * [FreeBSD](doc/HELPERS.md#freebsd)
  * [Installing from source](doc/HELPERS.md#installing-from-source)
    * [Automatic installation for RHEL/Debian/BSD](doc/HELPERS.md#automatic-installation-for-rheldebianbsd)
    * [Nginx package](doc/HELPERS.md#nginx-package)
    * [Dependencies](doc/HELPERS.md#dependencies)
    * [Patches](doc/HELPERS.md#patches)
    * [3rd party modules](doc/HELPERS.md#3rd-party-modules)
    * [Configure options](doc/HELPERS.md#cconfigure-options)
    * [Compiler and linker](doc/HELPERS.md#compiler-and-linker)
      * [Debugging Symbols](doc/HELPERS.md#debugging-symbols)
    * [SystemTap](doc/HELPERS.md#systemtap)
      * [stapxx](doc/HELPERS.md#stapxx)
    * [Installation Nginx on CentOS 7](doc/HELPERS.md#installation-nginx-on-centos-7)
      * [Pre installation tasks](doc/HELPERS.md#pre-installation-tasks)
      * [Dependencies](doc/HELPERS.md#dependencies)
      * [Get Nginx sources](doc/HELPERS.md#get-nginx-sources)
      * [Download 3rd party modules](doc/HELPERS.md#download-3rd-party-modules)
      * [Build Nginx](doc/HELPERS.md#build-nginx)
      * [Post installation tasks](doc/HELPERS.md#post-installation-tasks)
    * [Installation OpenResty on CentOS 7](doc/HELPERS.md#installation-openresty-on-centos-7)
    * [Installation Tengine on Ubuntu 18.04](doc/HELPERS.md#installation-tengine-on-ubuntu-1804)
    * [Installation Nginx on FreeBSD 11.3](doc/HELPERS.md#installation-nginx-on-freebsd-113)
    * [Installation Nginx on FreeBSD 11.3 from ports](doc/HELPERS.md#installation-nginx-on-freebsd-113-from-ports)
  * [Analyse configuration](doc/HELPERS.md#analyse-configuration)
  * [Monitoring](doc/HELPERS.md#monitoring)
    * [GoAccess](doc/HELPERS.md#goaccess)
      * [Build and install](doc/HELPERS.md#build-and-install)
      * [Analyse log file and enable all recorded statistics](doc/HELPERS.md#analyse-log-file-and-enable-all-recorded-statistics)
      * [Analyse compressed log file](doc/HELPERS.md#analyse-compressed-log-file)
      * [Analyse log file remotely](doc/HELPERS.md#analyse-log-file-remotely)
      * [Analyse log file and generate html report](doc/HELPERS.md#analyse-log-file-and-generate-html-report)
    * [Ngxtop](doc/HELPERS.md#ngxtop)
      * [Analyse log file](doc/HELPERS.md#analyse-log-file)
      * [Analyse log file and print requests with 4xx and 5xx](doc/HELPERS.md#analyse-log-file-and-print-requests-with-4xx-and-5xx)
      * [Analyse log file remotely](doc/HELPERS.md#analyse-log-file-remotely-1)
  * [Testing](doc/HELPERS.md#testing)
    * [Build OpenSSL 1.0.2-chacha version](doc/HELPERS.md#build-openssl-102-chacha-version)
    * [Send request and show response headers](doc/HELPERS.md#send-request-and-show-response-headers)
    * [Send request with http method, user-agent, follow redirects and show response headers](doc/HELPERS.md#send-request-with-http-method-user-agent-follow-redirects-and-show-response-headers)
    * [Send multiple requests](doc/HELPERS.md#send-multiple-requests)
    * [Testing SSL connection](doc/HELPERS.md#testing-ssl-connection)
    * [Testing SSL connection with SNI support](doc/HELPERS.md#testing-ssl-connection-with-sni-support)
    * [Testing SSL connection with specific SSL version](doc/HELPERS.md#testing-ssl-connection-with-specific-ssl-version)
    * [Testing SSL connection with specific cipher](doc/HELPERS.md#testing-ssl-connection-with-specific-cipher)
    * [Verify 0-RTT](doc/HELPERS.md#verify-0-rtt)
    * [Load testing with ApacheBench (ab)](doc/HELPERS.md#load-testing-with-apachebench-ab)
      * [Standard test](doc/HELPERS.md#standard-test)
      * [Test with Keep-Alive header](doc/HELPERS.md#test-with-keep-alive-header)
    * [Load testing with wrk2](doc/HELPERS.md#load-testing-with-wrk2)
      * [Standard scenarios](doc/HELPERS.md#standard-scenarios)
      * [POST call (with Lua)](doc/HELPERS.md#post-call-with-lua)
      * [Random paths (with Lua)](doc/HELPERS.md#random-paths-with-lua)
      * [Multiple paths (with Lua)](doc/HELPERS.md#multiple-paths-with-lua)
      * [Random server address to each thread (with Lua)](doc/HELPERS.md#random-server-address-to-each-thread-with-lua)
      * [Multiple json requests (with Lua)](doc/HELPERS.md#multiple-json-requests-with-lua)
      * [Debug mode (with Lua)](doc/HELPERS.md#debug-mode-with-lua)
      * [Analyse data pass to and from the threads](doc/HELPERS.md#analyse-data-pass-to-and-from-the-threads)
      * [Parsing wrk result and generate report](doc/HELPERS.md#parsing-wrk-result-and-generate-report)
    * [Load testing with locust](#load-testing-with-locust)
      * [Multiple paths](doc/HELPERS.md#multiple-paths)
      * [Multiple paths with different user sessions](doc/HELPERS.md#multiple-paths-with-different-user-sessions)
    * [TCP SYN flood Denial of Service attack](doc/HELPERS.md#tcp-syn-flood-denial-of-service-attack)
    * [HTTP Denial of Service attack](doc/HELPERS.md#tcp-syn-flood-denial-of-service-attack)
  * [Debugging](doc/HELPERS.md#debugging)
    * [Show information about processes](doc/HELPERS.md#show-information-about-nginx-processes)
    * [Check memory usage](doc/HELPERS.md#check-memoryusage)
    * [Show open files](doc/HELPERS.md#show-open-files)
    * [Dump configuration](doc/HELPERS.md#dump-configuration)
    * [Get the list of configure arguments](doc/HELPERS.md#get-the-list-of-configure-arguments)
    * [Check if the module has been compiled](doc/HELPERS.md#check-if-the-module-has-been-compiled)
    * [Show the most accessed IP addresses](doc/HELPERS.md#show-the-most-accessed-ip-addresses)
    * [Show the top 5 visitors (IP addresses)](doc/HELPERS.md#show-the-top-5-visitors-ip-addresses)
    * [Show the most requested urls](doc/HELPERS.md#show-the-most-requested-urls)
    * [Show the most requested urls containing 'string'](doc/HELPERS.md#show-the-most-requested-urls-containing-string)
    * [Show the most requested urls with http methods](doc/HELPERS.md#show-the-most-requested-urls-with-http-methods)
    * [Show the most accessed response codes](doc/HELPERS.md#show-the-most-accessed-response-codes)
    * [Analyse web server log and show only 2xx http codes](doc/HELPERS.md#analyse-web-server-log-and-show-only-2xx-http-codes)
    * [Analyse web server log and show only 5xx http codes](doc/HELPERS.md#analyse-web-server-log-and-show-only-5xx-http-codes)
    * [Show requests which result 502 and sort them by number per requests by url](doc/HELPERS.md#show-requests-which-result-502-and-sort-them-by-number-per-requests-by-url)
    * [Show requests which result 404 for php files and sort them by number per requests by url](doc/HELPERS.md#show-requests-which-result-404-for-php-files-and-sort-them-by-number-per-requests-by-url)
    * [Calculating amount of http response codes](doc/HELPERS.md#calculating-amount-of-http-response-codes)
    * [Calculating requests per second](doc/HELPERS.md#calculating-requests-per-second)
    * [Calculating requests per second with IP addresses](doc/HELPERS.md#calculating-requests-per-second-with-ip-addresses)
    * [Calculating requests per second with IP addresses and urls](doc/HELPERS.md#calculating-requests-per-second-with-ip-addresses-and-urls)
    * [Get entries within last n hours](doc/HELPERS.md#get-entries-within-last-n-hours)
    * [Get entries between two timestamps (range of dates)](doc/HELPERS.md#get-entries-between-two-timestamps-range-of-dates)
    * [Get line rates from web server log](doc/HELPERS.md#get-line-rates-from-web-server-log)
    * [Trace network traffic for all processes](doc/HELPERS.md#trace-network-traffic-for-all-nginx-processes)
    * [List all files accessed by a NGINX](doc/HELPERS.md#list-all-files-accessed-by-a-nginx)
    * [Check that the gzip_static module is working](doc/HELPERS.md#check-that-the-gzip_static-module-is-working)
    * [Which worker processing current request](doc/HELPERS.md#which-worker-processing-current-request)
    * [Capture only http packets](doc/HELPERS.md#capture-only-http-packets)
    * [Extract User Agent from the http packets](doc/HELPERS.md#extract-user-agent-from-the-http-packets)
    * [Capture only http GET and POST packets](doc/HELPERS.md#capture-only-http-get-and-post-packets)
    * [Capture requests and filter by source ip and destination port](doc/HELPERS.md#capture-requests-and-filter-by-source-ip-and-destination-port)
    * [Dump a process's memory](doc/HELPERS.md#dump-a-processs-memory)
    * [GNU Debugger (gdb)](doc/HELPERS.md#gnu-debugger-gdb)
      * [Dump configuration from a running process](doc/HELPERS.md#dump-configuration-from-a-running-process)
      * [Show debug log in memory](doc/HELPERS.md#show-debug-log-in-memory)
      * [Core dump backtrace](doc/HELPERS.md#core-dump-backtrace)
  * [Shell aliases](doc/HELPERS.md#shell-aliases)
  * [Configuration snippets](doc/HELPERS.md#configuration-snippets)
    * [Nginx server header removal](doc/HELPERS.md#nginx-server-header-removal)
    * [Custom log formats](doc/HELPERS.md#custom-log-formats)
    * [Log only 4xx/5xx](doc/HELPERS.md#log-only-4xx5xx)
    * [Restricting access with basic authentication](doc/HELPERS.md#restricting-access-with-basic-authentication)
    * [Restricting access with client certificate](doc/HELPERS.md#restricting-access-with-client-certificate)
    * [Restricting access by geographical location](doc/HELPERS.md#restricting-access-by-geographical-location)
      * [GeoIP 2 database](doc/HELPERS.md#geoip-2-database)
    * [Dynamic error pages with SSI](doc/HELPERS.md#dynamic-error-pages-with-ssi)
    * [Blocking/allowing IP addresses](doc/HELPERS.md#blockingallowing-ip-addresses)
    * [Blocking referrer spam](doc/HELPERS.md#blocking-referrer-spam)
    * [Limiting referrer spam](doc/HELPERS.md#limiting-referrer-spam)
    * [Limiting the rate of requests with burst mode](doc/HELPERS.md#limiting-the-rate-of-requests-with-burst-mode)
    * [Limiting the rate of requests with burst mode and nodelay](doc/HELPERS.md#limiting-the-rate-of-requests-with-burst-mode-and-nodelay)
    * [Limiting the rate of requests per IP with geo and map](doc/HELPERS.md#limiting-the-rate-of-requests-per-ip-with-geo-and-map)
    * [Limiting the number of connections](doc/HELPERS.md#limiting-the-number-of-connections)
    * [Using trailing slashes](doc/HELPERS.md#using-trailing-slashes)
    * [Properly redirect all HTTP requests to HTTPS](doc/HELPERS.md#properly-redirect-all-http-requests-to-https)
    * [Adding and removing the www prefix](doc/HELPERS.md#adding-and-removing-the-www-prefix)
    * [Proxy/rewrite and keep the original URL](doc/HELPERS.md#proxyrewrite-and-keep-the-original-url)
    * [Proxy/rewrite and keep the part of original URL](doc/HELPERS.md#proxyrewrite-and-keep-the-part-of-original-url)
    * [Proxy/rewrite without changing the original URL (in browser)](doc/HELPERS.md#proxyrewrite-without-changing-the-original-url-in-browser)
    * [Modify 301/302 response body](doc/HELPERS.md#modify-301302-response-body)
    * [Redirect POST request with payload to external endpoint](doc/HELPERS.md#redirect-post-request-with-payload-to-external-endpoint)
    * [Route to different backends based on HTTP method](doc/HELPERS.md#route-to-different-backends-based-on-HTTP-method)
    * [Allow multiple cross-domains using the CORS headers](doc/HELPERS.md#allow-multiple-cross-domains-using-the-cors-headers)
    * [Set correct scheme passed in X-Forwarded-Proto](doc/HELPERS.md#set-correct-scheme-passed-in-x-forwarded-proto)
  * [Other snippets](doc/HELPERS.md#other-snippets)
    * [Recreate base directory](doc/HELPERS.md#recreate-base-directory)
    * [Create a temporary static backend](doc/HELPERS.md#create-a-temporary-static-backend)
    * [Create a temporary static backend with SSL support](doc/HELPERS.md#create-a-temporary-static-backend-with-ssl-support)
    * [Generate password file with htpasswd command](doc/HELPERS.md#generate-password-file-with-htpasswd-command)
    * [Generate private key without passphrase](doc/HELPERS.md#generate-private-key-without-passphrase)
    * [Generate CSR](doc/HELPERS.md#generate-csr)
    * [Generate CSR (metadata from existing certificate)](doc/HELPERS.md#generate-csr-metadata-from-existing-certificate)
    * [Generate CSR with -config param](doc/HELPERS.md#generate-csr-with--config-param)
    * [Generate private key and CSR](doc/HELPERS.md#generate-private-key-and-csr)
    * [Generate ECDSA private key](doc/HELPERS.md#generate-ecdsa-private-key)
    * [Generate private key with CSR (ECC)](doc/HELPERS.md#generate-private-key-with-csr-ecc)
    * [Generate self-signed certificate](doc/HELPERS.md#generate-self-signed-certificate)
    * [Generate self-signed certificate from existing private key](doc/HELPERS.md#generate-self-signed-certificate-from-existing-private-key)
    * [Generate self-signed certificate from existing private key and csr](doc/HELPERS.md#generate-self-signed-certificate-from-existing-private-key-and-csr)
    * [Generate multidomain certificate](doc/HELPERS.md#generate-multidomain-certificate)
    * [Generate wildcard certificate](doc/HELPERS.md#generate-wildcard-certificate)
    * [Generate certificate with 4096 bit private key](doc/HELPERS.md#generate-certificate-with-4096-bit-private-key)
    * [Generate DH public parameters](doc/HELPERS.md#generate-dh-public-parameters)
    * [Display DH public parameters](doc/HELPERS.md#display-dh-public-parameters)
    * [Convert DER to PEM](doc/HELPERS.md#convert-der-to-pem)
    * [Convert PEM to DER](doc/HELPERS.md#convert-pem-to-der)
    * [Verification of the private key](doc/HELPERS.md#verification-of-the-private-key)
    * [Verification of the public key](doc/HELPERS.md#verification-of-the-public-key)
    * [Verification of the certificate](doc/HELPERS.md#verification-of-the-certificate)
    * [Verification of the CSR](doc/HELPERS.md#verification-of-the-csr)
    * [Check whether the private key and the certificate match](doc/HELPERS.md#check-whether-the-private-key-and-the-certificate-match)
- **[Base Rules (14)](doc/RULES.md#base-rules)**<a id="toc-base-rules"></a>
  * [Organising Nginx configuration](doc/RULES.md#beginner-organising-nginx-configuration)
  * [Format, prettify and indent your Nginx code](doc/RULES.md#beginner-format-prettify-and-indent-your-nginx-code)
  * [Use reload option to change configurations on the fly](doc/RULES.md#beginner-use-reload-option-to-change-configurations-on-the-fly)
  * [Separate listen directives for 80 and 443](doc/RULES.md#beginner-separate-listen-directives-for-80-and-443)
  * [Define the listen directives explicitly with address:port pair](doc/RULES.md#beginner-define-the-listen-directives-explicitly-with-addressport-pair)
  * [Prevent processing requests with undefined server names](doc/RULES.md#beginner-prevent-processing-requests-with-undefined-server-names)
  * [Never use a hostname in a listen or upstream directives](doc/RULES.md#beginner-never-use-a-hostname-in-a-listen-or-upstream-directives)
  * [Use only one SSL config for the listen directive](doc/RULES.md#beginner-use-only-one-ssl-config-for-the-listen-directive)
  * [Use geo/map modules instead of allow/deny](doc/RULES.md#beginner-use-geomap-modules-instead-of-allowdeny)
  * [Map all the things...](doc/RULES.md#beginner-map-all-the-things)
  * [Set global root directory for unmatched locations](doc/RULES.md#beginner-set-global-root-directory-for-unmatched-locations)
  * [Use return directive for URL redirection (301, 302)](doc/RULES.md#beginner-use-return-directive-for-url-redirection-301-302)
  * [Configure log rotation policy](doc/RULES.md#beginner-configure-log-rotation-policy)
  * [Don't duplicate index directive, use it only in the http block](doc/RULES.md#beginner-dont-duplicate-index-directive-use-it-only-in-the-http-block)
- **[Debugging (4)](doc/RULES.md#debugging)**<a id="toc-debugging"></a>
  * [Use custom log formats](doc/RULES.md#beginner-use-custom-log-formats)
  * [Use debug mode to track down unexpected behaviour](doc/RULES.md#beginner-use-debug-mode-to-track-down-unexpected-behaviour)
  * [Disable daemon, master process, and all workers except one](doc/RULES.md#beginner-disable-daemon-master-process-and-all-workers-except-one)
  * [Use core dumps to figure out why NGINX keep crashing](doc/RULES.md#beginner-use-core-dumps-to-figure-out-why-nginx-keep-crashing)
- **[Performance (11)](doc/RULES.md#performance)**<a id="toc-performance"></a>
  * [Adjust worker processes](doc/RULES.md#beginner-adjust-worker-processes)
  * [Use HTTP/2](doc/RULES.md#beginner-use-http2)
  * [Maintaining SSL sessions](doc/RULES.md#beginner-maintaining-ssl-sessions)
  * [Use exact names in a server_name directive where possible](doc/RULES.md#beginner-use-exact-names-in-a-server_name-directive-where-possible)
  * [Avoid checks server_name with if directive](doc/RULES.md#beginner-avoid-checks-server_name-with-if-directive)
  * [Use $request_uri to avoid using regular expressions](doc/RULES.md#beginner-use-request_uri-to-avoid-using-regular-expressions)
  * [Use try_files directive to ensure a file exists](doc/RULES.md#beginner-use-try_files-directive-to-ensure-a-file-exists)
  * [Use return directive instead of rewrite for redirects](doc/RULES.md#beginner-use-return-directive-instead-of-rewrite-for-redirects)
  * [Enable PCRE JIT to speed up processing of regular expressions](doc/RULES.md#beginner-enable-pcre-jit-to-speed-up-processing-of-regular-expressions)
  * [Make an exact location match to speed up the selection process](doc/RULES.md#beginner-make-an-exact-location-match-to-speed-up-the-selection-process)
  * [Use limit_conn to improve limiting the download speed](doc/RULES.md#beginner-use-limit_conn-to-improve-limiting-the-download-speed)
- **[Hardening (28)](doc/RULES.md#hardening)**<a id="toc-hardening"></a>
  * [Always keep NGINX up-to-date](doc/RULES.md#beginner-always-keep-nginx-up-to-date)
  * [Run as an unprivileged user](doc/RULES.md#beginner-run-as-an-unprivileged-user)
  * [Disable unnecessary modules](doc/RULES.md#beginner-disable-unnecessary-modules)
  * [Protect sensitive resources](doc/RULES.md#beginner-protect-sensitive-resources)
  * [Hide Nginx version number](doc/RULES.md#beginner-hide-nginx-version-number)
  * [Hide Nginx server signature](doc/RULES.md#beginner-hide-nginx-server-signature)
  * [Hide upstream proxy headers](doc/RULES.md#beginner-hide-upstream-proxy-headers)
  * [Force all connections over TLS](doc/RULES.md#beginner-force-all-connections-over-tls)
  * [Use only the latest supported OpenSSL version](doc/RULES.md#beginner-use-only-the-latest-supported-openssl-version)
  * [Use min. 2048-bit private keys](doc/RULES.md#beginner-use-min-2048-bit-private-keys)
  * [Keep only TLS 1.3 and TLS 1.2](doc/RULES.md#beginner-keep-only-tls-13-and-tls-12)
  * [Use only strong ciphers](doc/RULES.md#beginner-use-only-strong-ciphers)
  * [Use more secure ECDH Curve](doc/RULES.md#beginner-use-more-secure-ecdh-curve)
  * [Use strong Key Exchange with Perfect Forward Secrecy](doc/RULES.md#beginner-use-strong-key-exchange-with-perfect-forward-secrecy)
  * [Prevent Replay Attacks on Zero Round-Trip Time](doc/RULES.md#beginner-prevent-replay-attacks-on-zero-round-trip-time)
  * [Defend against the BEAST attack](doc/RULES.md#beginner-defend-against-the-beast-attack)
  * [Mitigation of CRIME/BREACH attacks](doc/RULES.md#beginner-mitigation-of-crimebreach-attacks)
  * [HTTP Strict Transport Security](doc/RULES.md#beginner-http-strict-transport-security)
  * [Reduce XSS risks (Content-Security-Policy)](doc/RULES.md#beginner-reduce-xss-risks-content-security-policy)
  * [Control the behaviour of the Referer header (Referrer-Policy)](doc/RULES.md#beginner-control-the-behaviour-of-the-referer-header-referrer-policy)
  * [Provide clickjacking protection (X-Frame-Options)](doc/RULES.md#beginner-provide-clickjacking-protection-x-frame-options)
  * [Prevent some categories of XSS attacks (X-XSS-Protection)](doc/RULES.md#beginner-prevent-some-categories-of-xss-attacks-x-xss-protection)
  * [Prevent Sniff Mimetype middleware (X-Content-Type-Options)](doc/RULES.md#beginner-prevent-sniff-mimetype-middleware-x-content-type-options)
  * [Deny the use of browser features (Feature-Policy)](doc/RULES.md#beginner-deny-the-use-of-browser-features-feature-policy)
  * [Reject unsafe HTTP methods](doc/RULES.md#beginner-reject-unsafe-http-methods)
  * [Prevent caching of sensitive data](doc/RULES.md#beginner-prevent-caching-of-sensitive-data)
  * [Control Buffer Overflow attacks](doc/RULES.md#beginner-control-buffer-overflow-attacks)
  * [Mitigating Slow HTTP DoS attacks (Closing Slow Connections)](doc/RULES.md#beginner-mitigating-slow-http-dos-attacks-closing-slow-connections)
- **[Reverse Proxy (7)](doc/RULES.md#reverse-proxy)**<a id="toc-reverse-proxy"></a>
  * [Use pass directive compatible with backend protocol](doc/RULES.md#beginner-use-pass-directive-compatible-with-backend-protocol)
  * [Be careful with trailing slashes in proxy_pass directive](doc/RULES.md#beginner-be-careful-with-trailing-slashes-in-proxy_pass-directive)
  * [Set and pass Host header only with $host variable](doc/RULES.md#beginner-set-and-pass-host-header-only-with-host-variable)
  * [Set properly values of the X-Forwarded-For header](doc/RULES.md#beginner-set-properly-values-of-the-x-forwarded-for-header)
  * [Don't use X-Forwarded-Proto with $scheme behind reverse proxy](doc/RULES.md#beginner-dont-use-x-forwarded-proto-with-scheme-behind-reverse-proxy)
  * [Always pass Host, X-Real-IP, and X-Forwarded headers to the backend](doc/RULES.md#beginner-always-pass-host-x-real-ip-and-x-forwarded-headers-to-the-backend)
  * [Use custom headers without X- prefix](doc/RULES.md#beginner-use-custom-headers-without-x--prefix)
- **[Load Balancing (2)](doc/RULES.md#load-balancing)**<a id="toc-load-balancing"></a>
  * [Tweak passive health checks](doc/RULES.md#beginner-tweak-passive-health-checks)
  * [Don't disable backends by comments, use down parameter](doc/RULES.md#beginner-dont-disable-backends-by-comments-use-down-parameter)
- **[Others (2)](doc/RULES.md#others)**<a id="toc-others"></a>
  * [Enable DNS CAA Policy](doc/RULES.md#beginner-enable-dns-caa-policy)
  * [Define security policies with security.txt](doc/RULES.md#beginner-define-security-policies-with-securitytxt)
- **[Configuration Examples](doc/EXAMPLES.md#configuration-examples)**<a id="toc-configuration-examples"></a>
  * [Reverse Proxy](doc/EXAMPLES.md#reverse-proxy)
    * [Installation](doc/EXAMPLES.md#installation)
    * [Configuration](doc/EXAMPLES.md#configuration)
    * [Import configuration](doc/EXAMPLES.md#import-configuration)
    * [Set bind IP address](doc/EXAMPLES.md#set-bind-ip-address)
    * [Set your domain name](doc/EXAMPLES.md#set-your-domain-name)
    * [Regenerate private keys and certs](doc/EXAMPLES.md#regenerate-private-keys-and-certs)
    * [Update modules list](doc/EXAMPLES.md#update-modules-list)
    * [Generating the necessary error pages](doc/EXAMPLES.md#generating-the-necessary-error-pages)
    * [Add new domain](doc/EXAMPLES.md#add-new-domain)
    * [Test your configuration](doc/EXAMPLES.md#test-your-configuration)

</details>

# Introduction

<br>

<p align="center">
  <a href="https://www.nginx.com/">
    <img src="https://github.com/trimstray/nginx-admins-handbook/blob/master/static/img/nginx_admins_handbook_logo.png">
  </a>
</p>

<br>

  > Before you start playing with NGINX please read an official **[Beginner’s Guide](http://nginx.org/en/docs/beginners_guide.html)**. It's a great introduction for everyone.

**Nginx** (_/ˌɛndʒɪnˈɛks/ EN-jin-EKS_, stylized as NGINX or nginx) is an open source HTTP and reverse proxy server, a mail proxy server, and a generic TCP/UDP proxy server. It is originally written by [Igor Sysoev](http://sysoev.ru/en/). For a long time, it has been running on many heavily loaded Russian sites including Yandex, Mail.Ru, VK, and Rambler. In the April 2019 NGINX was the most commonly used HTTP server (see [Netcraft survey](https://news.netcraft.com/archives/category/web-server-survey/)).

NGINX is a fast, light-weight and powerful web server that can also be used as a:

- fast HTTP reverse proxy
- reliable load balancer
- high performance caching server
- full-fledged web platform

Generally, it provides the core of complete web stacks and is designed to help build scalable web applications. When it comes to performance, NGINX can easily handle a huge amount of traffic. The other main advantage of the NGINX is that allows you to do the same thing in different ways.

For me, it is a one of the best and most important service that I used in my SysAdmin career.

----

These essential documents should be the main source of knowledge for you:

- **[Getting Started](https://www.nginx.com/resources/wiki/start/)**
- **[NGINX Documentation](https://nginx.org/en/docs/)**
- **[Development guide](http://nginx.org/en/docs/dev/development_guide.html)**

In addition, I would like to recommend three great docs focuses on the concept of the HTTP protocol:

- **[HTTP Made Really Easy](https://www.jmarshall.com/easy/http/)**
- **[Hypertext Transfer Protocol Specification](https://www.w3.org/Protocols/)**
- **[Web technology for developers - HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP)**

If you love security keep your eye on this one: [Cryptology ePrint Archive](https://eprint.iacr.org/). It provides access to recent research in cryptology and explores many subjects of security (e.g. Ciphers, Algorithms, SSL/TLS protocols). I also recommend to read [Bulletproof SSL and TLS](https://www.feistyduck.com/books/bulletproof-ssl-and-tls/). Yep, it's definitely the most comprehensive book about deploying TLS for me.

## Prologue

When I was studying architecture of HTTP servers I became interested in NGINX. I found a lot of information about it but I've never found one guide that covers the most important things in a suitable form. I was a little disappointed.

I was interested in everything: NGINX internals, functions, security best practices, performance optimisations, tips & tricks, hacks and rules, but for me all documents treated the subject lightly.

Of course, [Official Documentation](https://nginx.org/en/docs/) is the best place but I know that we also have other great resources:

- [agentzh's Nginx Tutorials](https://openresty.org/download/agentzh-nginx-tutorials-en.html)
- [Nginx Guts](http://www.nginxguts.com/)
- [Nginx discovery journey](http://www.nginx-discovery.com/)
- [Emiller’s Guide To Nginx Module Development](https://www.evanmiller.org/nginx-modules-guide.html)
- [Emiller’s Advanced Topics In Nginx Module Development](https://www.evanmiller.org/nginx-modules-guide-advanced.html)

These are definitely the best assets for us and in the first place you should seek help there.

Moreover, in order to improve your knowledge please see [Books](#books) chapter. It contains top literature on NGINX.

## Why I Created This Handbook

For me, however, there hasn't been a truly in-depth and reasonably simple cheatsheet which describe a variety of configurations and important cross-cutting topics for HTTP servers. I think, the configuration you provided should work without any talisman. That's why I created this repository.

  > This handbook is a collection of rules, helpers, notes, papers, best practices, and recommendations gathered and used by me (also in production environments). Many of them refer to external resources.

There are a lot of things you can do to improve NGINX server and this guide will attempt to cover as many of them as possible.

Throughout this handbook you will explore the many features and capabilities of the NGINX. You'll find out, for example, how to testing the performance or how to resolve debugging problems. You will learn configuration guidelines, security design patterns, ways to handle common issues and how to stay out of them. I explained here a few best tips to avoid pitfalls and configuration mistakes.

In this handbook I added set of guidelines and examples has also been produced to help you administer of the NGINX. They give us insight into NGINX internals also.

Mostly, I apply the rules presented here on the NGINX working as a reverse proxy. However, does not to prevent them being implemented for NGINX as a standalone server.

## Who This Handbook is For

If you do not have the time to read hundreds of articles (just like me) this multipurpose handbook may be useful. I created it in the hope that it will be useful especially for System Administrators and Experts of web-based applications. I think it can also be a good complement to official documentation.

I did my best to make this handbook a single and consistent. Is organized in an order that makes logical sense to me. Of course, I still have a lot [to improve and to do](#contributing--support). I hope you enjoy it, and fun with it.

## Before You Start

Remember about the following most important things:

  > **`Do not follow guides just to get 100% of something. Think about what you actually do at your server!`**

  > **`There are no settings that are perfect for everyone.`**

  > **`The only correct approach is to understand your exposure, measure and tune.`**

  > **`These guidelines provides (in some places) recommendations for very restrictive setup.`**

<br>

<p align="center">
  <img src="https://github.com/trimstray/nginx-admins-handbook/blob/master/static/img/crypto_nerds.png">
</p>

## Contributing & Support

  > _A real community, however, exists only when its members interact in a meaningful way that deepens their understanding of each other and leads to learning._

If you find something which doesn't make sense, or something doesn't seem right, please make a pull request and please add valid and well-reasoned explanations about your changes or comments.

Before adding a pull request, please see the **[contributing guidelines](CONTRIBUTING.md)**.

If this project is useful and important for you, you can bring **positive energy** by giving some **good words** or **supporting this project**. Thank you!

What needs to be done? Look at the following ToDo list:

New chapters:

- [x] **Bonus Stuff**
- [x] **HTTP Basics**
- [x] **SSL/TLS Basics**
- [x] **Reverse Proxy**
- [ ] **Caching**
- [x] **3rd party modules**
- [ ] **Web Application Firewall**
- [ ] **ModSecurity**
- [x] **Debugging**

Existing chapters:

<details>
<summary><b>Introduction</b></summary><br>

  - [x] _Prologue_
  - [x] _Why I Created This Handbook_
  - [x] _Who This Handbook is For_
  - [x] _Before You Start_
  - [x] _Contributing & Support_
  - [x] _Checklist to rule them all_

</details>

<details>
<summary><b>Bonus Stuff</b></summary><br>

  - [x] _Fully automatic installation_
  - [x] _Static error pages generator_

</details>

<details>
<summary><b>Books</b></summary><br>

  - [x] _ModSecurity 3.0 and NGINX: Quick Start Guide_
  - [x] _Cisco ACE to NGINX: Migration Guide_

</details>

<details>
<summary><b>External Resources</b></summary><br>

  - _Nginx official_
    - [x] _Nginx Forum_
    - [x] _Nginx Mailing List_
    - [x] _NGINX-Demos_
  - _Presentations & Videos_
    - [x] _NGINX: Basics and Best Practices_
    - [x] _NGINX Installation and Tuning_
    - [x] _Nginx Internals (by Joshua Zhu)_
    - [x] _Nginx internals (by Liqiang Xu)_
    - [x] _How to secure your web applications with NGINX_
    - [x] _Tuning TCP and NGINX on EC2_
    - [x] _Extending functionality in nginx, with modules!_
    - [x] _Nginx - Tips and Tricks._
    - [x] _Nginx Scripting - Extending Nginx Functionalities with Lua_
    - [x] _How to handle over 1,200,000 HTTPS Reqs/Min_
    - [x] _Using ngx_lua / lua-nginx-module in pixiv_
  - _Static analyzers_
    - [x] _nginx-minify-conf_
  - _Comparison reviews_
    - [x] _NGINX vs. Apache (Pro/Con Review, Uses, & Hosting for Each)_
    - [x] _Web cache server performance benchmark: nuster vs nginx vs varnish vs squid_
  - _Builder tools_
    - [x] _Nginx-builder_
  - _Benchmarking tools_
    - [x] _wrk2_
    - [x] _httperf_
    - [x] _slowloris_
    - [x] _slowhttptest_
    - [x] _GoldenEye_
  - _Debugging tools_
    - [x] _strace_
    - [x] _GDB_
    - [x] _SystemTap_
    - [x] _stapxx_
    - [x] _htrace.sh_
  - _Other stuff_
    - [x] _OWASP Cheat Sheet Series_
    - [x] _Mozilla Web Security_
    - [x] _Application Security Wiki_
    - [x] _OWASP ASVS 4.0_
    - [x] _The System Design Primer_
    - [x] _awesome-scalability_
    - [x] _Web Architecture 101_

</details>

<details>
<summary><b>HTTP Basics</b></summary><br>

  - [x] _Features and architecture_
  - [x] _URI vs URL_
  - [x] _HTTP Headers_
  - [x] _HTTP Methods_
  - [x] _Request_
    - [x] _Request line_
      - [x] _Methods_
      - [x] _Request URI_
      - [x] _HTTP version_
    - [x] _Request header fields_
    - [x] _Message body_
    - [x] _Generate requests_
  - [x] _Response_
    - [x] _Status line_
      - [x] _HTTP version_
      - [x] _Status codes and reason phrase_
    - [x] _Response header fields_
    - [x] _Message body_

</details>

<details>
<summary><b>SSL/TLS Basics</b></summary><br>

  - [x] _TLS versions_
  - [x] _TLS handshake_
  - [x] _Cipher suites_
  - [x] _Diffie-Hellman key exchange_

</details>

<details>
<summary><b>NGINX Basics</b></summary><br>

  - _Configuration syntax_
    - [x] _Comments_
    - [x] _End of lines_
    - [x] _Variables, Strings, and Quotes_
    - [x] _Directives, Blocks, and Contexts_
    - [x] _External files_
    - [x] _Measurement units_
    - [x] _Regular expressions with PCRE_
    - [x] _Enable syntax highlighting_
  - _Connection processing_
    - [x] _Event-Driven architecture_
    - [x] _Multiple processes_
    - [x] _Simultaneous connections_
    - [x] _HTTP Keep-Alive connections_
  - _Server blocks logic_
    - [x] _Matching location_
      - [ ] _if in location_
      - [ ] _Nested locations_
    - [x] _rewrite vs return_
    - [x] _try_files directive_
    - [x] _if, break and set_
    - [x] _root vs alias_
    - [x] _internal directive_
    - [x] _External and internal redirects_
  - _Log files_
    - [x] _Conditional logging_
    - [x] _Manually log rotation_
  - _Reverse proxy_
    - [x] _Passing requests_
    - [x] _Trailing slashes_
    - [x] _Processing headers_
    - [x] _Passing headers_
      - [x] _Importance of the Host header_
      - [x] _Redirects and X-Forwarded-Proto_
      - [x] _A warning about the X-Forwarded-For_
      - [x] _Improve extensibility with Forwarded_
  - _Load balancing algorithms_
    - [x] _Backend parameters_
    - [x] _Upstream servers with SSL_
    - [x] _Round Robin_
    - [x] _Weighted Round Robin_
    - [x] _Least Connections_
    - [x] _Weighted Least Connections_
    - [x] _IP Hash_
    - [x] _Generic Hash_
    - [ ] _Fair module_
    - [x] _Other methods_
  - _Rate Limiting_
    - [x] _Variables_
    - [x] _Directives, keys, and zones_
    - [x] _Burst and nodelay parameters_
  - _3rd party modules_
    - [x] _ngx_set_misc_
    - [x] _ngx_http_geoip_module_

</details>

<details>
<summary><b>Helpers</b></summary><br>

  - _Installing from source_
    - [x] _Automatic installation for RHEL/Debian/BSD_
    - [x] _Compiler and linker_
      - [x] _Debugging Symbols_
    - [x] _SystemTap_
      - [x] _stapxx_
    - [x] _Separation and improvement of installation methods_
    - [x] _Installation Nginx on CentOS 7_
    - [x] _Installation OpenResty on CentOS 7_
    - [x] _Installation Tengine on Ubuntu 18.04_
    - [x] _Installation Nginx on FreeBSD 11.3_
    - [x] _Installation Nginx on FreeBSD 11.3 from ports_
  - _Monitoring_
    - [ ] _CollectD, Prometheus, and Grafana_
      - [ ] _nginx-vts-exporter_
    - [ ] _CollectD, InfluxDB, and Grafana_
    - [ ] _Telegraf, InfluxDB, and Grafana_
  - _Testing_
    - [x] _Build OpenSSL 1.0.2-chacha version_
    - [x] _Send request and show response headers_
    - [x] _Send request with http method, user-agent, follow redirects and show response headers_
    - [x] _Send multiple requests_
    - [x] _Testing SSL connection_
    - [x] _Testing SSL connection with SNI support_
    - [x] _Testing SSL connection with specific SSL version_
    - [x] _Testing SSL connection with specific cipher_
    - [x] _Verify 0-RTT_
    - _Load testing with ApacheBench (ab)_
      - [x] _Standard test_
      - [x] _Test with Keep-Alive header_
    - _Load testing with wrk2_
      - [x] _Standard scenarios_
      - [x] _POST call (with Lua)_
      - [x] _Random paths (with Lua)_
      - [x] _Multiple paths (with Lua)_
      - [x] _Random server address to each thread (with Lua)_
      - [x] _Multiple json requests (with Lua)_
      - [x] _Debug mode (with Lua)_
      - [x] _Analyse data pass to and from the threads_
      - [x] _Parsing wrk result and generate report_
    - _Load testing with locust_
      - [x] _Multiple paths_
      - [x] _Multiple paths with different user sessions_
    - [x] _TCP SYN flood Denial of Service attack_
    - [x] _HTTP Denial of Service attack_
  - _Debugging_
    - [x] _Show information about processes_
    - [x] _Check memory usage_
    - [x] _Show open files_
    - [x] _Dump configuration_
    - [x] _Get the list of configure arguments_
    - [x] _Check if the module has been compiled_
    - [x] _Show the most requested urls with http methods_
    - [x] _Show the most accessed response codes_
    - [x] _Calculating requests per second with IP addresses and urls_
    - [x] _Check that the gzip_static module is working_
    - [x] _Which worker processing current request_
    - [x] _Capture only http packets_
    - [x] _Extract User Agent from the http packets_
    - [x] _Capture only http GET and POST packets_
    - [x] _Capture requests and filter by source ip and destination port_
    - [ ] _Server Side Include (SSI) debugging_
    - [x] _Dump a process's memory_
    - _GNU Debugger (gdb)_
      - [x] _Dump configuration from a running process_
      - [x] _Show debug log in memory_
      - [x] _Core dump backtrace_
    - _SystemTap cheatsheet_
      - [x] _stapxx_
  - _Errors & Issues_
    - [ ] _Common errors_
  - _Configuration snippets_
    - [x] _Nginx server header removal_
    - [x] _Custom log formats_
    - [x] _Log only 4xx/5xx_
    - [x] _Restricting access with client certificate_
    - [x] _Restricting access by geographical location_
      - [x] _GeoIP 2 database_
    - [ ] _Custom error pages_
    - [x] _Dynamic error pages with SSI_
    - [x] _Limiting the rate of requests per IP with geo and map_
    - [x] _Using trailing slashes_
    - [x] _Properly redirect all HTTP requests to HTTPS_
    - [x] _Adding and removing the www prefix_
    - [x] _Proxy/rewrite and keep the original URL_
    - [x] _Proxy/rewrite and keep the part of original URL_
    - [x] _Proxy/rewrite without changing the original URL (in browser)_
    - [x] _Modify 301/302 response body_
    - [x] _Redirect POST request with payload to external endpoint_
    - [x] _Route to different backends based on HTTP method_
    - [x] _Allow multiple cross-domains using the CORS headers_
    - [x] _Set correct scheme passed in X-Forwarded-Proto_
    - [ ] _Tips and methods for high load traffic testing (cheatsheet)_
    - [ ] _Location matching examples_
    - [ ] _Passing requests to the backend_
      - [ ] _The HTTP backend server_
      - [ ] _The uWSGI backend server_
      - [ ] _The FastCGI backend server_
      - [ ] _The memcached backend server_
      - [ ] _The Redis backend server_
    - [ ] _HTTPS traffic to upstream servers_
    - [ ] _TCP and UDP load balancing_
    - [ ] _Lua snippets_
    - [ ] _nginscripts snippets_
  - _Other snippets_
    - [x] _Recreate base directory_
    - [x] _Create a temporary static backend_
    - [x] _Create a temporary static backend with SSL support_
    - [x] _Generate password file with htpasswd command_
    - [x] _Generate private key without passphrase_
    - [x] _Generate CSR_
    - [x] _Generate CSR (metadata from existing certificate)_
    - [x] _Generate CSR with -config param_
    - [x] _Generate private key and CSR_
    - [x] _Generate ECDSA private key_
    - [x] _Generate private key with CSR (ECC)_
    - [x] _Generate self-signed certificate_
    - [x] _Generate self-signed certificate from existing private key_
    - [x] _Generate self-signed certificate from existing private key and csr_
    - [x] _Generate multidomain certificate_
    - [x] _Generate wildcard certificate_
    - [x] _Generate certificate with 4096 bit private key_
    - [x] _Generate DH public parameters_
    - [x] _Display DH public parameters_
    - [x] _Convert DER to PEM_
    - [x] _Convert PEM to DER_
    - [x] _Verification of the private key_
    - [x] _Verification of the public key_
    - [x] _Verification of the certificate_
    - [x] _Verification of the CSR_
    - [x] _Check whether the private key and the certificate match_

</details>

<details>
<summary><b>Base Rules</b></summary><br>

  - [x] _Format, prettify and indent your Nginx code_
  - [x] _Never use a hostname in a listen or upstream directives_
  - [ ] _Making a rewrite absolute (with scheme)_
  - [x] _Use return directive for URL redirection (301, 302)_
  - [x] _Configure log rotation policy_
  - [x] _Don't duplicate index directive, use it only in the http block_

</details>

<details>
<summary><b>Debugging</b></summary><br>

  - [x] _Disable daemon, master process, and all workers except one_
  - [x] _Use core dumps to figure out why NGINX keep crashing_
  - [ ] _Use mirror module to copy requests to another backend_
  - [ ] _Dynamic debugging with echo module_
  - [ ] _Dynamic debugging with SSI_

</details>

<details>
<summary><b>Performance</b></summary><br>

  - [ ] _Avoid multiple index directives_
  - [x] _Use $request_uri to avoid using regular expressions_
  - [x] _Use try_files directive to ensure a file exists_
  - [ ] _Don't pass all requests to the backend - use try_files_
  - [x] _Use return directive instead of rewrite for redirects_
  - [x] _Enable PCRE JIT to speed up processing of regular expressions_
  - [ ] _Set proxy timeouts for normal load and under heavy load_
  - [ ] _Configure kernel parameters for high load traffic_

</details>

<details>
<summary><b>Hardening</b></summary><br>

  - [x] _Keep NGINX up-to-date_
  - [x] _Use only the latest supported OpenSSL version_
  - [x] _Prevent Replay Attacks on Zero Round-Trip Time_
  - [ ] _Enable OCSP Stapling_
  - [x] _Prevent caching of sensitive data_
  - [ ] _Set properly files and directories permissions (also with acls) on a paths_
  - [ ] _Implement HTTPOnly and secure attributes on cookies_

</details>

<details>
<summary><b>Reverse Proxy</b></summary><br>

  - [x] _Use pass directive compatible with backend protocol_
  - [x] _Be careful with trailing slashes in proxy_pass directive_
  - [x] _Set and pass Host header only with $host variable_
  - [x] _Set properly values of the X-Forwarded-For header_
  - [x] _Don't use X-Forwarded-Proto with $scheme behind reverse proxy_
  - [x] _Always pass Host, X-Real-IP, and X-Forwarded headers to the backend_
  - [x] _Use custom headers without X- prefix_
  - [ ] _Set proxy buffers and timeouts_

</details>

<details>
<summary><b>Others</b></summary><br>

  - [x] _Define security policies with security.txt_

</details>

If you have an idea, send it back to me or add a pull request.

## Checklist to rule them all

  > This checklist contains [all rules (68)](doc/RULES.md) from this handbook.

Generally, I think that each of these principles is important and should be considered. I tried, however, to separate them into four levels of priority which I hope will help guide your decision.

| <b>PRIORITY</b> | <b>NAME</b> | <b>AMOUNT</b> | <b>DESCRIPTION</b> |
| :---:        | :---         | :---:        | :---         |
| ![high](static/img/priorities/high.png) | <i>critical</i> | 28 | definitely use this rule, otherwise it will introduce high risks of your NGINX security, performance, and other |
| ![medium](static/img/priorities/medium.png) | <i>major</i> | 22 | it's also very important but not critical, and should still be addressed at the earliest possible opportunity |
| ![low](static/img/priorities/low.png) | <i>normal</i> | 12 | there is no need to implement but it is worth considering because it can improve the NGINX working and functions |
| ![info](static/img/priorities/info.png) | <i>minor</i> | 6 | as an option to implement or use (not required) |

Remember, these are only guidelines. My point of view may be different from yours so if you feel these priority levels do not reflect your configurations commitment to security, performance or whatever else, you should adjust them as you see fit.

| <b>RULE</b> | <b>CHAPTER</b> | <b>PRIORITY</b> |
| :---         | :---         | :---:        |
| [Define the listen directives explicitly with address:port pair](doc/RULES.md#beginner-define-the-listen-directives-explicitly-with-addressport-pair)<br><sup>Prevents soft mistakes which may be difficult to debug.</sup> | Base Rules | ![high](static/img/priorities/high.png) |
| [Prevent processing requests with undefined server names](doc/RULES.md#beginner-prevent-processing-requests-with-undefined-server-names)<br><sup>It protects against configuration errors, e.g. traffic forwarding to incorrect backends.</sup> | Base Rules | ![high](static/img/priorities/high.png) |
| [Never use a hostname in a listen or upstream directives](doc/RULES.md#beginner-never-use-a-hostname-in-a-listen-or-upstream-directives)<br><sup>While this may work, it will comes with a large number of issues.</sup> | Base Rules | ![high](static/img/priorities/high.png) |
| [Configure log rotation policy](doc/RULES.md#beginner-configure-log-rotation-policy)<br><sup>Save yourself trouble with your web server: configure appropriate logging policy.</sup> | Base Rules | ![high](static/img/priorities/high.png) |
| [Use HTTP/2](doc/RULES.md#beginner-use-http2)<br><sup>HTTP/2 will make our applications faster, simpler, and more robust.</sup> | Performance | ![high](static/img/priorities/high.png) |
| [Enable PCRE JIT to speed up processing of regular expressions](doc/RULES.md#beginner-enable-pcre-jit-to-speed-up-processing-of-regular-expressions)<br><sup>NGINX with PCRE JIT is much faster than without it.</sup> | Performance | ![high](static/img/priorities/high.png) |
| [Always keep NGINX up-to-date](doc/RULES.md#always-keep-nginx-up-to-date)<br><sup>Use newest NGINX package to fix vulnerabilities, bugs, and to use new features.</sup> | Hardening | ![high](static/img/priorities/high.png) |
| [Run as an unprivileged user](doc/RULES.md#beginner-run-as-an-unprivileged-user)<br><sup>Use the principle of least privilege. This way only master process runs as root.</sup> | Hardening | ![high](static/img/priorities/high.png) |
| [Protect sensitive resources](doc/RULES.md#beginner-protect-sensitive-resources)<br><sup>Hidden directories and files should never be web accessible.</sup> | Hardening | ![high](static/img/priorities/high.png) |
| [Hide upstream proxy headers](doc/RULES.md#beginner-hide-upstream-proxy-headers)<br><sup>Don't expose what version of software is running on the server.</sup> | Hardening | ![high](static/img/priorities/high.png) |
| [Force all connections over TLS](doc/RULES.md#beginner-force-all-connections-over-tls)<br><sup>Protects your website especially for handle sensitive communications.</sup> | Hardening | ![high](static/img/priorities/high.png) |
| [Use min. 2048-bit private keys](doc/RULES.md#beginner-use-min-2048-bit-private-keys)<br><sup>2048 bits private keys are sufficient for commercial use.</sup> | Hardening | ![high](static/img/priorities/high.png) |
| [Keep only TLS 1.3 and TLS 1.2](doc/RULES.md#beginner-keep-only-tls-13-and-tls-12)<br><sup>Use TLS with modern cryptographic algorithms and without protocol weaknesses.</sup> | Hardening | ![high](static/img/priorities/high.png) |
| [Use only strong ciphers](doc/RULES.md#beginner-use-only-strong-ciphers)<br><sup>Use only strong and not vulnerable cipher suites.</sup> | Hardening | ![high](static/img/priorities/high.png) |
| [Use more secure ECDH Curve](doc/RULES.md#beginner-use-more-secure-ecdh-curve)<br><sup>Use ECDH Curves with according to NIST recommendations.</sup> | Hardening | ![high](static/img/priorities/high.png) |
| [Use strong Key Exchange with Perfect Forward Secrecy](doc/RULES.md#beginner-use-strong-key-exchange-with-perfect-forward-secrecy)<br><sup>Establishes a shared secret between two parties that can be used for secret communication.</sup> | Hardening | ![high](static/img/priorities/high.png) |
| [Defend against the BEAST attack](doc/RULES.md#beginner-defend-against-the-beast-attack)<br><sup>The server ciphers should be preferred over the client ciphers.</sup> | Hardening | ![high](static/img/priorities/high.png) |
| [HTTP Strict Transport Security](doc/RULES.md#beginner-http-strict-transport-security)<br><sup>Tells browsers that it should only be accessed using HTTPS, instead of using HTTP.</sup> | Hardening | ![high](static/img/priorities/high.png) |
| [Reduce XSS risks (Content-Security-Policy)](doc/RULES.md#beginner-reduce-xss-risks-content-security-policy)<br><sup>CSP is best used as defence-in-depth. It reduces the harm that a malicious injection can cause.</sup> | Hardening | ![high](static/img/priorities/high.png) |
| [Control the behaviour of the Referer header (Referrer-Policy)](doc/RULES.md#beginner-control-the-behaviour-of-the-referer-header-referrer-policy)<br><sup>The default behaviour of referrer leaking puts websites at risk of privacy and security breaches.</sup> | Hardening | ![high](static/img/priorities/high.png) |
| [Provide clickjacking protection (X-Frame-Options)](doc/RULES.md#beginner-provide-clickjacking-protection-x-frame-options)<br><sup>Defends against clickjacking attack.</sup> | Hardening | ![high](static/img/priorities/high.png) |
| [Prevent some categories of XSS attacks (X-XSS-Protection)](doc/RULES.md#beginner-prevent-some-categories-of-xss-attacks-x-xss-protection)<br><sup>Prevents to render pages if a potential XSS reflection attack is detected.</sup> | Hardening | ![high](static/img/priorities/high.png) |
| [Prevent Sniff Mimetype middleware (X-Content-Type-Options)](doc/RULES.md#beginner-prevent-sniff-mimetype-middleware-x-content-type-options)<br><sup>Tells browsers not to sniff MIME types.</sup> | Hardening | ![high](static/img/priorities/high.png) |
| [Reject unsafe HTTP methods](doc/RULES.md#beginner-reject-unsafe-http-methods)<br><sup>Only allow the HTTP methods for which you, in fact, provide services.</sup> | Hardening | ![high](static/img/priorities/high.png) |
| [Prevent caching of sensitive data](doc/RULES.md#beginner-prevent-caching-of-sensitive-data)<br><sup>It helps to prevent critical data (e.g. credit card details, or username) leaked.</sup> | Hardening | ![high](static/img/priorities/high.png) |
| [Use pass directive compatible with backend protocol](doc/RULES.md#beginner-use-pass-directive-compatible-with-backend-protocol)<br><sup>Set pass directive only to working with compatible backend layer protocol.</sup> | Reverse Proxy | ![high](static/img/priorities/high.png) |
| [Set properly values of the X-Forwarded-For header](doc/RULES.md#beginner-set-properly-values-of-the-x-forwarded-for-header)<br><sup>Identify clients communicating with servers located behind the proxy.</sup> | Reverse Proxy | ![high](static/img/priorities/high.png) |
| [Don't use X-Forwarded-Proto with $scheme behind reverse proxy](doc/RULES.md#beginner-dont-use-x-forwarded-proto-with-scheme-behind-reverse-proxy)<br><sup>Prevent pass incorrect value of this header.</sup> | Reverse Proxy | ![high](static/img/priorities/high.png) |
| [Organising Nginx configuration](doc/RULES.md#beginner-organising-nginx-configuration)<br><sup>Well organised code is easier to understand and maintain.</sup> | Base Rules | ![medium](static/img/priorities/medium.png) |
| [Format, prettify and indent your Nginx code](doc/RULES.md#beginner-format-prettify-and-indent-your-nginx-code)<br><sup>Formatted code is easier to maintain, debug, and can be read and understood in a short amount of time.</sup> | Base Rules | ![medium](static/img/priorities/medium.png) |
| [Use reload option to change configurations on the fly](doc/RULES.md#beginner-use-reload-option-to-change-configurations-on-the-fly)<br><sup>Graceful reload of the configuration without stopping the server and dropping any packets.</sup> | Base Rules | ![medium](static/img/priorities/medium.png) |
| [Use return directive for URL redirection (301, 302)](doc/RULES.md#beginner-use-return-directive-for-url-redirection-301-302)<br><sup>The by far simplest and fastest because there is no regexp that has to be evaluated.</sup> | Base Rules | ![medium](static/img/priorities/medium.png) |
| [Maintaining SSL sessions](doc/RULES.md#beginner-maintaining-ssl-sessions)<br><sup>Improves performance from the clients’ perspective.</sup> | Performance | ![medium](static/img/priorities/medium.png) |
| [Use exact names in a server_name directive where possible](doc/RULES.md#beginner-use-exact-names-in-a-server_name-directive-where-possible)<br><sup>Helps speed up searching using exact names.</sup> | Performance | ![medium](static/img/priorities/medium.png) |
| [Avoid checks server_name with if directive](doc/RULES.md#beginner-avoid-checks-server_name-with-if-directive)<br><sup>It decreases NGINX processing requirements.</sup> | Performance | ![medium](static/img/priorities/medium.png) |
| [Use $request_uri to avoid using regular expressions](doc/RULES.md#beginner-use-request_uri-to-avoid-using-regular-expressions)<br><sup>By default, the regex is costly and will slow down the performance.</sup> | Performance | ![medium](static/img/priorities/medium.png) |
| [Use try_files directive to ensure a file exists](doc/RULES.md#beginner-use-try_files-directive-to-ensure-a-file-exists)<br><sup>Use it if you need to search for a file, it saving duplication of code also.</sup> | Performance | ![medium](static/img/priorities/medium.png) |
| [Use return directive instead of rewrite for redirects](doc/RULES.md#beginner-use-return-directive-instead-of-rewrite-for-redirects)<br><sup>Use return directive to more speedy response than rewrite.</sup> | Performance | ![medium](static/img/priorities/medium.png) |
| [Disable unnecessary modules](doc/RULES.md#beginner-disable-unnecessary-modules)<br><sup>Limits vulnerabilities, improve performance and memory efficiency.</sup> | Hardening | ![medium](static/img/priorities/medium.png) |
| [Hide Nginx version number](doc/RULES.md#beginner-hide-nginx-version-number)<br><sup>Don't disclose sensitive information about NGINX.</sup> | Hardening | ![medium](static/img/priorities/medium.png) |
| [Hide Nginx server signature](doc/RULES.md#beginner-hide-nginx-server-signature)<br><sup>Don't disclose sensitive information about NGINX.</sup> | Hardening | ![medium](static/img/priorities/medium.png) |
| [Use only the latest supported OpenSSL version](doc/RULES.md#beginner-use-only-the-latest-supported-openssl-version)<br><sup>Stay protected from SSL security threats and don't miss out new features.</sup> | Hardening | ![medium](static/img/priorities/medium.png) |
| [Prevent Replay Attacks on Zero Round-Trip Time](doc/RULES.md#beginner-prevent-replay-attacks-on-zero-round-trip-time)<br><sup>0-RTT is disabled by default but you should know that enabling this option creates a significant security risks.</sup> | Hardening | ![medium](static/img/priorities/medium.png) |
| [Mitigation of CRIME/BREACH attacks](doc/RULES.md#beginner-mitigation-of-crimebreach-attacks)<br><sup>Disable HTTP compression or compress only zero sensitive content.</sup> | Hardening | ![medium](static/img/priorities/medium.png) |
| [Deny the use of browser features (Feature-Policy)](doc/RULES.md#beginner-deny-the-use-of-browser-features-feature-policy)<br><sup>A mechanism to allow and deny the use of browser features.</sup> | Hardening | ![medium](static/img/priorities/medium.png) |
| [Control Buffer Overflow attacks](doc/RULES.md#beginner-control-buffer-overflow-attacks)<br><sup>Prevents errors are characterised by the overwriting of memory fragments of the NGINX process.</sup> | Hardening | ![medium](static/img/priorities/medium.png) |
| [Mitigating Slow HTTP DoS attacks (Closing Slow Connections)](doc/RULES.md#beginner-mitigating-slow-http-dos-attack-closing-slow-connections)<br><sup>Prevents attacks in which the attacker sends HTTP requests in pieces slowly.</sup> | Hardening | ![medium](static/img/priorities/medium.png) |
| [Set and pass Host header only with $host variable](doc/RULES.md#beginner-set-and-pass-host-header-only-with-host-variable)<br><sup>Use of the $host is the only one guaranteed to have something sensible.</sup> | Reverse Proxy | ![medium](static/img/priorities/medium.png) |
| [Always pass Host, X-Real-IP, and X-Forwarded headers to the backend](doc/RULES.mdbeginner-always-pass-host-x-real-ip-and-x-forwarded-headers-to-the-backend)<br><sup>It gives you more control of forwarded headers.</sup> | Reverse Proxy | ![medium](static/img/priorities/medium.png) |
| [Enable DNS CAA Policy](doc/RULES.md#beginner-enable-dns-caa-policy)<br><sup>Allows domain name holders to indicate to CA whether they are authorized to issue digital certificates.</sup> | Others | ![medium](static/img/priorities/medium.png) |
| [Separate listen directives for 80 and 443](doc/RULES.md#beginner-separate-listen-directives-for-80-and-443)<br><sup>Help you maintain and modify your configuration.</sup> | Base Rules | ![low](static/img/priorities/low.png) |
| [Use only one SSL config for the listen directive](doc/RULES.md#beginner-use-only-one-ssl-config-for-the-listen-directive)<br><sup>The most of the SSL changes will affect only the default server.</sup> | Base Rules | ![low](static/img/priorities/low.png) |
| [Use geo/map modules instead of allow/deny](doc/RULES.md#beginner-use-geomap-modules-instead-of-allowdeny)<br><sup>Provides the perfect way to block invalid visitors.</sup> | Base Rules | ![low](static/img/priorities/low.png) |
| [Set global root directory for unmatched locations](doc/RULES.md#beginner-set-global-root-directory-for-unmatched-locations)<br><sup>Specifies the root directory for an undefined locations.</sup> | Base Rules | ![low](static/img/priorities/low.png) |
| [Don't duplicate index directive, use it only in the http block](doc/RULES.md#beginner-dont-duplicate-index-directive-use-it-only-in-the-http-block)<br><sup>Watch out for duplicating the same rules.</sup> | Base Rules | ![low](static/img/priorities/low.png) |
| [Adjust worker processes](doc/RULES.md#beginner-adjust-worker-processes)<br><sup>You can adjust this value to maximum throughput under high concurrency.</sup> | Performance | ![low](static/img/priorities/low.png) |
| [Make an exact location match to speed up the selection process](doc/RULES.md#beginner-make-an-exact-location-match-to-speed-up-the-selection-process)<br><sup>Exact location matches are often used to speed up the selection process.</sup> | Performance | ![low](static/img/priorities/low.png) |
| [Use limit_conn to improve limiting the download speed](doc/RULES.md#beginner-use-limit_conn-to-improve-limiting-the-download-speed)<br><sup>Limits NGINX download speed per connection.</sup> | Performance | ![low](static/img/priorities/low.png) |
| [Be careful with trailing slashes in proxy_pass directive](doc/RULES.md#beginner-be-careful-with-trailing-slashes-in-proxy_pass-directive)<br><sup>Incorrect setting could end up with some strange url.</sup> | Reverse Proxy | ![low](static/img/priorities/low.png) |
| [Use custom headers without X- prefix](doc/RULES.md#beginner-use-custom-headers-without-x--prefix)<br><sup>The use of custom headers with X- prefix is discouraged.</sup> | Reverse Proxy | ![low](static/img/priorities/low.png) |
| [Tweak passive health checks](doc/RULES.md#beginner-tweak-passive-health-checks)<br><sup>Improve behaviour of the passive health checks.</sup> | Load Balancing | ![low](static/img/priorities/low.png) |
| [Define security policies with security.txt](doc/RULES.md#beginner-define-security-policies-with-securitytxt)<br><sup>Helps make things easier for companies and security researchers.</sup> | Others | ![low](static/img/priorities/low.png) |
| [Map all the things...](doc/RULES.md#beginner-map-all-the-things)<br><sup>Map module provides a more elegant solution for clearly parsing a big list of regexes.</sup> | Base Rules | ![info](static/img/priorities/info.png) |
| [Use custom log formats](doc/RULES.md#beginner-use-custom-log-formats)<br><sup>This is extremely helpful for debugging specific location directives.</sup> | Debugging | ![info](static/img/priorities/info.png) |
| [Use debug mode to track down unexpected behaviour](doc/RULES.md#beginner-use-debug-mode-to-track-down-unexpected-behaviour)<br><sup>There's probably more detail than you want, but that can sometimes be a lifesaver.</sup> | Debugging | ![info](static/img/priorities/info.png) |
| [Disable daemon, master process, and all workers except one](doc/RULES.md#beginner-disable-daemon-master-process-and-all-workers-except-one)<br><sup>This simplifies the debugging and lets test configurations rapidly.</sup> | Debugging | ![info](static/img/priorities/info.png) |
| [Use core dumps to figure out why NGINX keep crashing](doc/RULES.md#beginner-use-core-dumps-to-figure-out-why-nginx-keep-crashing)<br><sup>Enable core dumps when your NGINX instance receive an unexpected error or when it crashed.</sup> | Debugging | ![info](static/img/priorities/info.png) |
| [Don't disable backends by comments, use down parameter](doc/RULES.md#beginner-dont-disable-backends-by-comments-use-down-parameter)<br><sup>Is a good solution to marks the server as permanently unavailable.</sup> | Load Balancing | ![info](static/img/priorities/info.png) |

# Bonus Stuff

Here you'll find a few of the different things I've worked and which included to this repository. I hope that these extras will be useful to you.

## Reports: blkcipher.info

Many of these recipes have been applied to the configuration of my private website.

  > An example configuration is in [configuration examples](#configuration-examples) chapter. It's also based on [this](https://github.com/trimstray/nginx-admins-handbook/blob/master/static/img/cheatsheets/nginx-hardening-cheatsheet-tls13.png) version of printable high-res hardening cheatsheets.

### SSL Labs

  > Read about SSL Labs grading [here](https://community.qualys.com/docs/DOC-6321-ssl-labs-grading-2018) (SSL Labs Grading 2018).

Short SSL Labs grades explanation:

  > _A+ is clearly the desired grade, both A and B grades are acceptable and result in adequate commercial security. The B grade, in particular, may be applied to configurations designed to support very wide audiences (for old clients)_.

I finally got **A+** grade and following scores:

- Certificate = **100%**
- Protocol Support = **100%**
- Key Exchange = **90%**
- Cipher Strength = **90%**

Look also at the following recommendations. In my opinion, the right configuration of NGINX should give the following SSL Labs scores:

- **Recommended**

  - A+
  - Certificate: 100/100
  - Protocol Support: 95/100
  - Key Exchange: 90/100
  - Cipher Strength: 90/100

- **Perfect but restrictive**

  - A+
  - Certificate: 100/100
  - Protocol Support: 100/100
  - Key Exchange: 100/100
  - Cipher Strength: 100/100

<p align="center">
  <a href="https://www.ssllabs.com/ssltest/analyze.html?d=blkcipher.info&hideResults=on">
    <img src="https://github.com/trimstray/nginx-admins-handbook/blob/master/static/img/blkcipher_ssllabs_preview.png" alt="blkcipher_ssllabs_preview">
  </a>
</p>

### Mozilla Observatory

  > Read about Mozilla Observatory [here](https://observatory.mozilla.org/faq/).

I also got the highest note on the Observatory:

<p align="center">
  <a href="https://observatory.mozilla.org/analyze/blkcipher.info?third-party=false">
    <img src="https://github.com/trimstray/nginx-admins-handbook/blob/master/static/img/blkcipher_mozilla_observatory_preview.png" alt="blkcipher_mozilla_observatory_preview">
  </a>
</p>

## Printable hardening cheatsheets

I created two versions of printable posters with hardening cheatsheets (High-Res 5000x8200) based on recipes from this handbook:

  > For `*.xcf` and `*.pdf` formats please see [this](https://github.com/trimstray/nginx-admins-handbook/tree/master/static/img) directory.

- **A+** with all **100%’s** on @ssllabs and **120/100** on @mozilla observatory:

  > It provides the highest scores of the SSL Labs test. Setup is very restrictive with 4096-bit private key, only TLS 1.2, and also modern strict TLS cipher suites (non 128-bits).

<p align="center">
  <img src="https://github.com/trimstray/nginx-admins-handbook/blob/master/static/img/cheatsheets/nginx-hardening-cheatsheet-tls12-100p.png" alt="nginx-hardening-cheatsheet-100p" width="92%" height="92%">
</p>

- **A+** on @ssllabs and **120/100** on @mozilla observatory with TLS 1.3 support:

  > It provides less restrictive setup with 2048-bit private key, TLS 1.3 and 1.2, and also modern strict TLS cipher suites (128/256-bits). The final grade is also in line with the industry standards. Recommend using this configuration.

<p align="center">
  <img src="https://github.com/trimstray/nginx-admins-handbook/blob/master/static/img/cheatsheets/nginx-hardening-cheatsheet-tls13.png" alt="nginx-hardening-cheatsheet-tls13" width="92%" height="92%">
</p>

## Fully automatic installation

I created a set of scripts for unattended installation of NGINX from the raw, uncompiled code. It allows you to easily install, create a setup for dependencies (like `zlib` or `openssl`), and customized with installation parameters.

For more information please see [Installing from source - Automatic installation](#automatic-installation) chapter.

## Static error pages generator

I created a simple to use generator for static pages with errors to replace the default error pages that comes with any web server like NGINX.

For more information please see [HTTP Static Error Pages Generator](https://github.com/trimstray/nginx-admins-handbook/tree/master/lib/nginx/snippets/http-error-pages#http-static-error-pages-generator).

# Books

#### [Nginx Essentials](https://www.amazon.com/Nginx-Essentials-Valery-Kholodkov/dp/1785289535)

Authors: **Valery Kholodkov**

_Excel in Nginx quickly by learning to use its most essential features in real-life applications._

- _Learn how to set up, configure, and operate an Nginx installation for day-to-day use_
- _Explore the vast features of Nginx to manage it like a pro, and use them successfully to run your website_
- _Example-based guide to get the best out of Nginx to reduce resource usage footprint_

<sup><i>This short review comes from this book or the store.</i></sup>

#### [Nginx Cookbook](https://www.oreilly.com/library/view/nginx-cookbook/9781492049098/)

Authors: **Derek DeJonghe**

_You’ll find recipes for:_

- _Traffic management and A/B testing_
- _Managing programmability and automation with dynamic templating and the NGINX Plus API_
- _Securing access through encrypted traffic, secure links, HTTP authentication subrequests, and more_
- _Deploying NGINX to AWS, Azure, and Google cloud-computing services_
- _Using Docker to deploy containers and microservices_
- _Debugging and troubleshooting, performance tuning, and practical ops tips_

<sup><i>This short review comes from this book or the store.</i></sup>

#### [Nginx HTTP Server](https://www.amazon.com/Nginx-HTTP-Server-Harness-infrastructure/dp/178862355X)

Authors: **Martin Fjordvald**, **Clement Nedelcu**

_Harness the power of Nginx to make the most of your infrastructure and serve pages faster than ever._

- _Discover possible interactions between Nginx and Apache to get the best of both worlds_
- _Learn to exploit the features offered by Nginx for your web applications_
- _Get your hands on the most updated version of Nginx (1.13.2) to support all your web administration requirements_

<sup><i>This short review comes from this book or the store.</i></sup>

#### [Nginx High Performance](https://www.amazon.com/Nginx-High-Performance-Rahul-Sharma/dp/1785281836)

Authors: **Rahul Sharma**

_Optimize NGINX for high-performance, scalable web applications._

- _Configure Nginx for best performance, with configuration examples and explanations_
- _Step-by-step tutorials for performance testing using open source software_
- _Tune the TCP stack to make the most of the available infrastructure_

<sup><i>This short review comes from this book or the store.</i></sup>

#### [Mastering Nginx](https://www.amazon.com/Mastering-Nginx-Dimitri-Aivaliotis/dp/1849517444)

Authors: **Dimitri Aivaliotis**

_Written for experienced systems administrators and engineers, this book teaches you from scratch how to configure Nginx for any situation. Step-by-step instructions and real-world code snippets clarify even the most complex areas._

<sup><i>This short review comes from this book or the store.</i></sup>

#### [ModSecurity 3.0 and NGINX: Quick Start Guide](https://www.nginx.com/resources/library/modsecurity-3-nginx-quick-start-guide/)

Authors: **Faisal Memon**, **Owen Garrett**, **Michael Pleshakov**

_Learn in this ebook how to get started with ModSecurity, the world’s most widely deployed web application firewall (WAF), now available for NGINX and NGINX Plus._

<sup><i>This short review comes from this book or the store.</i></sup>

#### [Cisco ACE to NGINX: Migration Guide](https://www.nginx.com/resources/library/cisco-ace-nginx-migration-guide/)

Authors: **Faisal Memon**

_This ebook provides step-by-step instructions on replacing Cisco ACE with NGINX and off-the-shelf servers. NGINX helps you cut costs and modernize._

_In this ebook you will learn:_

- _How to migrate Cisco ACE configuration to NGINX, with detailed examples_
- _Why you should go with a software load balancer, and not hardware_

<sup><i>This short review comes from this book or the store.</i></sup>

# External Resources

##### Nginx official

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://www.nginx.com/"><b>Nginx Project</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://nginx.org/en/docs/"><b>Nginx Documentation</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.nginx.com/resources/wiki/"><b>Nginx Wiki</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://docs.nginx.com/nginx/admin-guide/"><b>Nginx Admin's Guide</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.nginx.com/resources/wiki/start/topics/tutorials/config_pitfalls/"><b>Nginx Pitfalls and Common Mistakes</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="http://nginx.org/en/docs/dev/development_guide.html"><b>Development guide</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://forum.nginx.org/"><b>Nginx Forum</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://mailman.nginx.org/mailman/listinfo/nginx"><b>Nginx Mailing List</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/nginx/nginx"><b>Nginx Read-only Mirror</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/nginxinc/NGINX-Demos"><b>NGINX-Demos
</b></a><br>
</p>

##### Nginx distributions

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://openresty.org/"><b>OpenResty</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://tengine.taobao.org/"><b>The Tengine Web Server</b></a><br>
</p>

##### Comparison reviews

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://www.hostingadvice.com/how-to/nginx-vs-apache/"><b>NGINX vs. Apache (Pro/Con Review, Uses, & Hosting for Each)</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/jiangwenyuan/nuster/wiki/Web-cache-server-performance-benchmark:-nuster-vs-nginx-vs-varnish-vs-squid"><b>Web cache server performance benchmark: nuster vs nginx vs varnish vs squid</b></a><br>
</p>

##### Cheatsheets & References

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://openresty.org/download/agentzh-nginx-tutorials-en.html"><b>agentzh's Nginx Tutorials</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="http://agentzh.org/misc/slides/nginx-conf-scripting/nginx-conf-scripting.html#1"><b>Introduction to nginx.conf scripting</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="http://www.nginx-discovery.com/"><b>Nginx discovery journey</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="http://www.nginxguts.com/"><b>Nginx Guts</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://gist.github.com/carlessanagustin/9509d0d31414804da03b"><b>Nginx Cheatsheet</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="http://www.scalescale.com/tips/nginx/"><b>Nginx Tutorials, Linux Sysadmin Configuration & Optimizing Tips and Tricks</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/h5bp/server-configs-nginx"><b>Nginx boilerplate configs</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/nginx-boilerplate/nginx-boilerplate"><b>Awesome Nginx configuration template</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/SimulatedGREG/nginx-cheatsheet"><b>Nginx Quick Reference</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/fcambus/nginx-resources"><b>A collection of resources covering Nginx and more</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/lebinh/nginx-conf"><b>A collection of useful Nginx configuration snippets</b></a><br>
</p>

##### Performance & Hardening

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/denji/nginx-tuning"><b>Nginx Tuning For Best Performance by Denji</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://istlsfastyet.com/"><b>TLS has exactly one performance problem: it is not used widely enough</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.ssllabs.com/projects/best-practices/"><b>SSL/TLS Deployment Best Practices</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.ssllabs.com/projects/rating-guide/index.html"><b>SSL Server Rating Guide</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.upguard.com/blog/how-to-build-a-tough-nginx-server-in-15-steps"><b>How to Build a Tough NGINX Server in 15 Steps</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.cyberciti.biz/tips/linux-unix-bsd-nginx-webserver-security.html"><b>Top 25 Nginx Web Server Best Security Practices</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://calomel.org/nginx.html"><b>Nginx Secure Web Server</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://cipherli.st/"><b>Strong ciphers for Apache, Nginx, Lighttpd and more</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://raymii.org/s/tutorials/Strong_SSL_Security_On_nginx.html"><b>Strong SSL Security on Nginx</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://enable-cors.org/index.html"><b>Enable cross-origin resource sharing (CORS)</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/nbs-system/naxsi"><b>NAXSI - WAF for Nginx</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://geekflare.com/install-modsecurity-on-nginx/"><b>ModSecurity for Nginx</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.owasp.org/index.php/Transport_Layer_Protection_Cheat_Sheet"><b>Transport Layer Protection Cheat Sheet</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://wiki.mozilla.org/Security/Server_Side_TLS"><b>Security/Server Side TLS</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://caniuse.com/#home"><b>Browser support tables for modern web technologies</b></a><br>
</p>

##### Presentations & Videos

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://www.slideshare.net/Nginx/nginx-basics-and-best-practices"><b>NGINX: Basics and Best Practices</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.slideshare.net/Nginx/nginx-installation-and-tuning"><b>NGINX Installation and Tuning</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.slideshare.net/joshzhu/nginx-internals"><b>Nginx Internals (by Joshua Zhu)</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.slideshare.net/feifengxlq/nginx-internals-10514355"><b>Nginx internals (by Liqiang Xu)</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.slideshare.net/wallarm/how-to-secure-your-web-applications-with-nginx"><b>How to secure your web applications with NGINX</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.slideshare.net/chartbeat/tuning-tcp-and-nginx-on-ec2"><b>Tuning TCP and NGINX on EC2</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.slideshare.net/trygvevea/extending-functionality-in-nginx-with-modules"><b>Extending functionality in nginx, with modules!</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.slideshare.net/tuxtoti/nginx-tips-and-tricks-13087831"><b>Nginx - Tips and Tricks.</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.slideshare.net/TonyFabeen/nginx-scripting-extending-nginx-functionalities-with-lua"><b>Nginx Scripting - Extending Nginx Functionalities with Lua</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.slideshare.net/kazeburo/advanced-nginx-in-mercari-how-to-handle-over-1200000-https-reqsmin"><b>How to handle over 1,200,000 HTTPS Reqs/Min</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.slideshare.net/harukayon/ngx-lua-public"><b>Using ngx_lua / lua-nginx-module in pixiv</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.youtube.com/playlist?list=PLGz_X9w9raXewvc6tjIGGFZ6DBKHEld3k"><b>NGINX Conf 2014</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.youtube.com/playlist?list=PLGz_X9w9raXdED9BR6GQ61A6d3fBzjpbn"><b>NGINX Conf 2015</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.youtube.com/playlist?list=PLGz_X9w9raXcOsB_dT26iu0BvbSxWYG1g"><b>NGINX Conf 2016</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.youtube.com/playlist?list=PLGz_X9w9raXeT-z_rcZ9yF0kV5SENZ-yt"><b>NGINX Conf 2017</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.youtube.com/playlist?list=PLGz_X9w9raXeHhKRX6ZS7vmFKN12iYOw9"><b>NGINX Conf 2018 | Deep Dive Track</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.youtube.com/playlist?list=PLGz_X9w9raXe_Vc708VKvr5KJ4gnf1WxS"><b>NGINX Conf 2018 | Keynotes and Sessions</b></a><br>
</p>

##### Playgrounds

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/sportebois/nginx-rate-limit-sandbox"><b>NGINX Rate Limit, Burst and nodelay sandbox</b></a><br>
</p>

##### Config generators

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://nginxconfig.io/"><b>Nginx config generator on steroids</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://mozilla.github.io/server-side-tls/ssl-config-generator/"><b>Mozilla SSL Configuration Generator</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/linkedin/nginx-config-builder"><b>nginx-config-builder</b></a> - is a python library for constructing nginx configuration files.<br>
</p>

##### Static analyzers

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/yandex/gixy"><b>gixy</b></a> - is a tool to analyze Nginx configuration to prevent security misconfiguration and automate flaw detection.<br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/1connect/nginx-config-formatter"><b>nginx-config-formatter</b></a> - Nginx config file formatter/beautifier written in Python.<br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/vasilevich/nginxbeautifier"><b>nginxbeautifier</b></a> - format and beautify Nginx config files.<br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/lovette/nginx-tools/tree/master/nginx-minify-conf"><b>nginx-minify-conf</b></a> - creates a minified version of a Nginx configuration.<br>
</p>

##### Log analyzers

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://goaccess.io/"><b>GoAccess</b></a> - is a fast, terminal-based log analyzer (quickly analyze and view web server statistics in real time).<br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.graylog.org/"><b>Graylog</b></a> - is a leading centralized log management for capturing, storing, and enabling real-time analysis.<br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.elastic.co/products/logstash"><b>Logstash</b></a> - is an open source, server-side data processing pipeline.<br>
</p>

##### Performance analyzers

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/lebinh/ngxtop"><b>ngxtop</b></a> - parses your Nginx access log and outputs useful, top-like, metrics of your Nginx server.<br>
</p>

##### Builder tools

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/TinkoffCreditSystems/Nginx-builder"><b>Nginx-builder</b></a> - is a tool for building deb or rpm package NGINX from the source code.<br>
</p>

##### Benchmarking tools

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://httpd.apache.org/docs/2.4/programs/ab.html"><b>ab</b></a> - is a single-threaded command line tool for measuring the performance of HTTP web servers.<br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.joedog.org/siege-home/"><b>siege</b></a> - is an http load testing and benchmarking utility.<br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/wg/wrk"><b>wrk</b></a> - is a modern HTTP benchmarking tool capable of generating significant load.<br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/giltene/wrk2"><b>wrk2</b></a> - is a constant throughput, correct latency recording variant of wrk.<br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/codesenberg/bombardier"><b>bombardier</b></a> - is a HTTP(S) benchmarking tool.<br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/cmpxchg16/gobench"><b>gobench</b></a> - is a HTTP/HTTPS load testing and benchmarking tool.<br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/rakyll/hey"><b>hey</b></a> - is a HTTP load generator, ApacheBench (ab) replacement, formerly known as rakyll/boom.<br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/tarekziade/boom"><b>boom</b></a> - is a script you can use to quickly smoke-test your web app deployment.<br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/tarekziade/httperf"><b>httperf</b></a> - the httperf HTTP load generator.<br>
&nbsp;&nbsp;:black_small_square: <a href="https://jmeter.apache.org/"><b>JMeter™</b></a> - is designed to load test functional behavior and measure performance.<br>
&nbsp;&nbsp;:black_small_square: <a href="https://gatling.io/"><b>Gatling</b></a> - is a powerful open-source load and performance testing tool for web applications.<br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/locustio/locust"><b>locust</b></a> - is an easy-to-use, distributed, user load testing tool.<br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/gkbrk/slowloris"><b>slowloris</b></a> - low bandwidth DoS tool. Slowloris rewrite in Python.<br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/shekyan/slowhttptest"><b>slowhttptest</b></a> - application layer DoS attack simulator.<br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/jseidl/GoldenEye"><b>GoldenEye</b></a> - GoldenEye Layer 7 (KeepAlive+NoCache) DoS test tool.<br>
</p>

##### Debugging tools

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://strace.io/"><b>strace</b></a> - is a diagnostic, debugging and instructional userspace utility (linux syscall tracer) for Linux.<br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.gnu.org/software/gdb/"><b>GDB</b></a> - allows you to see what is going on `inside' another program while it executes.<br>
&nbsp;&nbsp;:black_small_square: <a href="https://sourceware.org/systemtap/"><b>SystemTap</b></a> - provides infrastructure to simplify the gathering of information about the running Linux system.<br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/openresty/stapxx"><b>stapxx</b></a> - simple macro language extensions to SystemTap.<br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/trimstray/htrace.sh"><b>htrace.sh</b></a> - is a simple Swiss Army knife for http/https troubleshooting and profiling.<br>
</p>

##### Development

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://www.lua.org/pil/contents.html"><b>Programming in Lua (first edition)</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="http://www.londonlua.org/scripting_nginx_with_lua/"><b>Scripting Nginx with Lua</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.evanmiller.org/nginx-modules-guide.html"><b>Emiller’s Guide To Nginx Module Development</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="http://www.evanmiller.org/nginx-modules-guide-advanced.html"><b>Emiller’s Advanced Topics In Nginx Module Development</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.airpair.com/nginx/extending-nginx-tutorial"><b>NGINX Tutorial: Developing Modules</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.openmymind.net/An-Introduction-To-OpenResty-Nginx-Lua/"><b>An Introduction To OpenResty (nginx + lua) - Part 1</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.openmymind.net/An-Introduction-To-OpenResty-Part-2/"><b>An Introduction To OpenResty - Part 2 - Concepts</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.openmymind.net/An-Introduction-To-OpenResty-Part-3/"><b>An Introduction To OpenResty - Part 3</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://blog.dutchcoders.io/openresty-with-dynamic-generated-certificates/"><b>OpenResty (Nginx) with dynamically generated certificates</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/openresty/programming-openresty"><b>Programming OpenResty</b></a><br>
</p>

##### Online tools

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://www.ssllabs.com/ssltest/"><b>SSL Server Test by SSL Labs</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.ssllabs.com/ssltest/viewMyClient.html"><b>SSL/TLS Capabilities of Your Browser</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.htbridge.com/ssl/"><b>Test SSL/TLS (PCI DSS, HIPAA and NIST)</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://sslanalyzer.comodoca.com/"><b>SSL analyzer and certificate checker</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://cryptcheck.fr/"><b>Test your TLS server configuration (e.g. ciphers)</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.jitbit.com/sslcheck/"><b>Scan your website for non-secure content</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://2ton.com.au/dhtool/"><b>Public Diffie-Hellman Parameter Service/Tool</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://securityheaders.com/"><b>Analyse the HTTP response headers by Security Headers</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://observatory.mozilla.org/"><b>Analyze your website by Mozilla Observatory</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://sslmate.com/caa/"><b>CAA Record Helper</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://webhint.io/"><b>Linting tool that will help you with your site's accessibility, speed, security and more</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://urlscan.io/"><b>Service to scan and analyse websites</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.url-encode-decode.com/"><b>Tool from above to either encode or decode a string of text</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://uncoder.io/"><b>Online translator for search queries on log data</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://regex101.com/"><b>Online regex tester and debugger: PHP, PCRE, Python, Golang and JavaScript</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://regexr.com/"><b>Online tool to learn, build, & test Regular Expressions</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.regextester.com/"><b>Online Regex Tester & Debugger</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/nginxinc/NGINX-Demos/tree/master/nginx-regex-tester"><b>nginx-regex-tester</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://gchq.github.io/CyberChef/"><b>A web app for encryption, encoding, compression and data analysis</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://nginx.viraptor.info/"><b>Nginx location match tester</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://detailyang.github.io/nginx-location-match-visible/"><b>Nginx location match visible</b></a><br>
</p>

##### Other stuff

<p>
&nbsp;&nbsp;:black_small_square: <a href="https://developer.mozilla.org/en-US/docs/Web"><b>Web technology for developers</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://cheatsheetseries.owasp.org/"><b>OWASP Cheat Sheet Series</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://infosec.mozilla.org/guidelines/web_security.html"><b>Mozilla Web Security</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://appsecwiki.com/#/"><b>Application Security Wiki</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/OWASP/ASVS/tree/master/4.0"><b>OWASP ASVS 4.0</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.iana.org/assignments/tls-parameters/tls-parameters.xhtml"><b>Transport Layer Security (TLS) Parameters</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://wiki.mozilla.org/Security/Server_Side_TLS"><b>Security/Server Side TLS by Mozilla</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/GrrrDog/TLS-Redirection#technical-details"><b>TLS Redirection (and Virtual Host Confusion)</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.acunetix.com/blog/articles/tls-vulnerabilities-attacks-final-part/"><b>TLS Security 6: Examples of TLS Vulnerabilities and Attacks</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.veracode.com/blog/2014/03/guidelines-for-setting-security-headers"><b>Guidelines for Setting Security Headers</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://medium.freecodecamp.org/secure-your-web-application-with-these-http-headers-fd66e0367628"><b>Secure your web application with these HTTP headers</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://zinoui.com/blog/security-http-headers"><b>Security HTTP Headers</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/GrrrDog/weird_proxies/wiki"><b>Analysis of various reverse proxies, cache proxies, load balancers, etc.</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.regular-expressions.info/"><b>Regular-Expressions</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://nickcraver.com/blog/2017/05/22/https-on-stack-overflow/#the-beginning"><b>HTTPS on Stack Overflow: The End of a Long Road</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://www.aosabook.org/en/nginx.html"><b>The Architecture of Open Source Applications - Nginx</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="http://www.bbc.co.uk/blogs/internet/entries/17d22fb8-cea2-49d5-be14-86e7a1dcde04"><b>BBC Digital Media Distribution: How we improved throughput by 4x</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="http://www.kegel.com/c10k.html"><b>The C10K problem by Dan Kegel</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="http://highscalability.com/blog/2013/5/13/the-secret-to-10-million-concurrent-connections-the-kernel-i.html"><b>The Secret To 10 Million Concurrent Connections</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://hpbn.co/"><b>High Performance Browser Networking</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/donnemartin/system-design-primer"><b>The System Design Primer</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/binhnguyennus/awesome-scalability"><b>awesome-scalability</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://engineering.videoblocks.com/web-architecture-101-a3224e126947"><b>Web Architecture 101</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://github.com/leandromoreira/linux-network-performance-parameters"><b>Learn where some of the network sysctl variables fit into the Linux/Kernel network flow</b></a><br>
&nbsp;&nbsp;:black_small_square: <a href="https://suniphrase.wordpress.com/2015/10/27/jemalloc-vs-tcmalloc-vs-dlmalloc/"><b>jemalloc vs tcmalloc vs dlmalloc</b></a><br>
</p>

# What's next?

Go to the [Table of Contents](#table-of-contents) or read the next chapters:

- **[HTTP Basics](doc/HTTP_BASICS.md#http-basics)**
  > Something about HTTP.
- **[SSL/TLS Basics](doc/SSL_TLS_BASICS.md#ssltls-basics)**
  > Something about SSL/TLS.
- **[NGINX Basics](doc/NGINX_BASICS.md#nginx-basics)**
  > Explanation of the NGINX mechanisms.
- **[Helpers](doc/HELPERS.md#helpers)**
  > One-liners, commands, utilities for building NGINX, and more
- **[Base Rules (14)](doc/RULES.md#base-rules)**
  > The basic set of rules to keep NGINX in good condition.
- **[Debugging (4)](doc/RULES.md#debugging)**
  > A few things for troubleshooting configuration problems.
- **[Performance (11)](doc/RULES.md#performance)**
  > Many methods to make sure the NGINX as fast as possible.
- **[Hardening (28)](doc/RULES.md#hardening)**
  > Hardening approaches and security standards.
- **[Reverse Proxy (7)](doc/RULES.md#reverse-proxy)**
  > A few rules about the NGINX proxy server.
- **[Load Balancing (2)](doc/RULES.md#load-balancing)**
  > You may improve of some rules about the NGINX working as a load balancer.
- **[Others (2)](doc/RULES.md#others)**
  > Something about other interesting rules.
- **[Configuration Examples](doc/EXAMPLES.md#configuration-examples)**
  > Here are some configuration examples.
