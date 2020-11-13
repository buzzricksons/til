# HSTS (HTTP Strict Transport Security)
HSTS (HTTP Strict Transport Security)란 브라우저가 HTTPS만을 사용하도록 강제하는 보안기능입니다. HSTS가 활성화된 후 HTTP 요청을 하게 되면 강제로 HTTPS로 전환되게 됩니다.
사용자들이 브라우저 주소를 입력 할 때 http:// 주소를 타이핑 하거나 혹은 https://를 생략하는 경향이 있는데, HSTS를 통해 HTTPS를 강제할 수 있게 됩니다.

HSTS는 다음과 같은 HTTP 헤더를 추가함으로서 활성화할 수 있습니다. 
Strict-Transport-Security: max-age=16070400; includeSubDomains

HTTP 통신에서는 브라우저가 HSTS 헤더를 무시합니다. HTTP 통신에서는 해커가 HSTS 헤더를 마음대로 조작할 수 있기 때문입니다.
HSTS는 Chrome, Firefox, Safari, Opera, Edge, IE11 등 대부분의 브라우저에서 지원합니다. (HSTS 브라우저 지원)

# X-XSS-Protection
HTTP X-XSS-Protection헤더는 Internet Explorer, Chrome 및 Safari에서 제공하는 기능으로서, (XSS) 공격을 감지 할 때 페이지 로드를 중지시킬 수 있습니다. 최신 브라우저에서는 Inline Javascript('unsafe-inline')사용을 못하게 하는 CSP(Content-Security-Policy) 보호기능이 있으나, 해당 기능을 지원하지 않는 구형 웹브라우저에서 사용자를 보호 할수 있는 기능을 제공할 수 있습니다.

```
X-XSS-Protection: 0
X-XSS-Protection: 1
X-XSS-Protection: 1; mode=block
X-XSS-Protection: 1; report=<reporting-uri>
```

* 0
    * XSS 필터링을 비활성화합니다.
* 1
    * XSS 필터링을 사용합니다 (일반적으로 브라우저의 기본값입니다). 사이트 내에서 스크립팅 공격이 감지되면 브라우저는 안전하지 않은 영역을 제거 후에 렌더링을 하게 됩니다.
* 1; mode=block
    * XSS 필터링을 사용합니다. 공격이 탐지되면 안전하지 않는 영역을 제거하는게 아니라, 페이지 렌더링을 중단합니다.
* 1; report=<reporting-URI>  (Chromium에서만 사용 가능)
    * XSS 필터링을 사용합니다. XSS 공격을 탐지하면 브라우저는 페이지 렌더링을 차단하고 위반 사항을 보고합니다. 이것은 CSP report-uri 지시문의 기능을 사용하여 보고서를 보냅니다.
