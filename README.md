# Fibaro Home Center Lite API Spec
Official API documentation: https://manuals.fibaro.com/knowledge-base-browse/rest-api/

The device itself exposes some API spec at `<fibaro-hc-root-endpoint>/docs/`.

## Logs
Some guides for fetching logs:
- https://intuitech.de/fibaro-hc2-hcl-log-dateien-auslesen/
- https://www.mkshb.de/fibaro-logs-auslesen/

## Reboot

### Sceniario:

* Ping to the gateway is successful locally
* whenever there is no data from Fibaro endpoints, then it maybe because one of the services in Fibaro HCL gateway is constantly rebooting. The error from fibaro can be like this:

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"><html ng-app="homeCenterApplication" ng-cloak><head><title>Home Center Lite 503 {{ TXT_HTTPERROR_503 }}</title><meta http-equiv="Content-type" content="application/xhtml+xml; charset=utf-8"><link rel="apple-touch-icon" sizes="57x57" href="/fibaro/favicons/apple-touch-icon-57x57.png"><link rel="apple-touch-icon" sizes="60x60" href="/fibaro/favicons/apple-touch-icon-60x60.png"><link rel="apple-touch-icon" sizes="72x72" href="/fibaro/favicons/apple-touch-icon-72x72.png"><link rel="apple-touch-icon" sizes="76x76" href="/fibaro/favicons/apple-touch-icon-76x76.png"><link rel="apple-touch-icon" sizes="114x114" href="/fibaro/favicons/apple-touch-icon-114x114.png"><link rel="apple-touch-icon" sizes="120x120" href="/fibaro/favicons/apple-touch-icon-120x120.png"><link rel="apple-touch-icon" sizes="144x144" href="/fibaro/favicons/apple-touch-icon-144x144.png"><link rel="apple-touch-icon" sizes="152x152" href="/fibaro/favicons/apple-touch-icon-152x152.png"><link rel="apple-touch-icon" sizes="180x180" href="/fibaro/favicons/apple-touch-icon-180x180.png"><link rel="icon" type="image/png" href="/fibaro/favicons/favicon-32x32.png" sizes="32x32"><link rel="icon" type="image/png" href="/fibaro/favicons/android-chrome-192x192.png" sizes="192x192"><link rel="icon" type="image/png" href="/fibaro/favicons/favicon-96x96.png" sizes="96x96"><link rel="icon" type="image/png" href="/fibaro/favicons/favicon-16x16.png" sizes="16x16"><link rel="manifest" href="/fibaro/favicons/manifest.js?version=1593518855488on"><link rel="mask-icon" href="/fibaro/favicons/safari-pinned-tab.svg" color="#5bbad5"><link rel="shortcut icon" href="/fibaro/favicons/favicon.ico"><meta name="msapplication-TileColor" content="#268ed5"><meta name="msapplication-TileImage" content="/fibaro/favicons/mstile-144x144.png"><meta name="msapplication-config" content="/fibaro/favicons/browserconfig.xml"><meta name="theme-color" content="#ffffff"><link rel="stylesheet" href="../style.css?version=1593518855488" type="text/css"><link rel="stylesheet" href="css/style_503.css?version=1593518855488" type="text/css"><link rel="stylesheet" href="../menu_style.css?version=1593518855488" type="text/css"><link rel="stylesheet" href="../cpanelstyle.css?version=1593518855488" type="text/css"><link rel="stylesheet" href="../ww.css?version=1593518855488" type="text/css"><link rel="stylesheet" href="../loading.css?version=1593518855488" type="text/css"><link rel="stylesheet" href="../scene_style.css?version=1593518855488" type="text/css"><link rel="stylesheet" href="../jquery.mobile-1.1.0.min.css?version=1593518855488"><script type="text/javascript" src="../lib/jquery/jquery-1.7.2.min.js?version=1593518855488"></script><script type="text/javascript" src="../lib/angularjs/angular-1.3.11.min.js?version=1593518855488"></script><script type="text/javascript" src="../js/translation.js?version=1593518855488"></script><script type="text/javascript" src="../js/tools.js?version=1593518855488"></script><script type="text/javascript" src="../js/config.js?version=1593518855488"></script><script type="text/javascript" src="../js/checkServiceStatus.js?version=1593518855488"></script><script type="text/javascript" src="../js/designer.js?version=1593518855488"></script><script type="text/javascript" src="../../configuration/js/general.js?version=1593518855488"></script><link rel="stylesheet" href="../login.css?version=1593518855488" type="text/css"></head><body ng-controller="homeCenterController" onload="checkServiceStatus( getURLParameter( 'trackBack' ) || globalLang + '/' + currentCategory + '/' + currentPage + location.search, true, true )"><div id="transparentOverlayLoading" class="transparentOverlayLoading displayNone"><section class="main"><ul class="bokeh"><li></li><li></li><li></li><li></li></ul></section></div><div class="error_bg_503"><a class="button_503_1" href="/fibaro/index.html">{{ TXT_HTTPERROR_REFRESH }}</a> <a class="button_503_2" href="#" onclick="generalReset( true ); return false">{{ TXT_HTTPERROR_SERVICES_RESTART }}</a></div></body></html>
```

or
```json
{"<html>\r\n<head><title>504 Gateway Time-out</title></head>\r\n<body bgcolor=\"white\">\r\n<center><h1>504 Gateway Time-out</h1></center>\r\n<hr><center>nginx/1.8.0</center>\r\n</body>\r\n</html>\r\n","url":"http://192.168.1.2/api/panels/event?deviceID=13&from=1614270936&to=1614351000"}
```
### Solution:
Reboot the gateway within the local network:
```bash
curl --location --request POST 'http://192.168.1.2/api/service/reboot' --header 'Authorization: Basic <base64-encoded-credentials>' --header 'Content-Length:0'
```
