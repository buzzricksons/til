# $_SERVER(サーバー変数) の種類

| 変数 | 説明 |
|:------------- |:-------------|
| $_SERVER['PHP_SELF'] | 現在実行しているスクリプトのファイル名です。 ドキュメントルートから取得されます。 例えば、http://example.com/test.php/foo.bar というアドレス上にあるスクリプトでは $_SERVER['PHP_SELF'] は /test.php/foo.bar となります。 __FILE__ 定数 には、カレント(すなわち読み込まれた)ファイルのパスとファイル名が含まれます。 PHP がコマンドラインから実行される場合、PHP 4.3.0 以降、 この変数にはスクリプト名が含まれます。これより前のバージョンでは、 この変数は使用できません。 |
| $_SERVER['GATEWAY_INTERFACE'] | サーバが使用している CGI のバージョンです。 例 'CGI/1.1' |
| $_SERVER['SERVER_ADDR'] | 現在のスクリプトが実行されているサーバの IP アドレスです。 |
| $_SERVER['SERVER_NAME'] | 現在のスクリプトが実行されているサーバのホスト名です。 スクリプトがバーチャルホスト上で実行されている場合は そのバーチャルホスト名となります。 |
| $_SERVER['SERVER_SOFTWARE'] | レスポンスヘッダ上に書かれている、 サーバの認識文字列です。 |
| $_SERVER['SERVER_PROTOCOL'] | ページがリクエストされた際のプロトコル名とバージョンです。 例.'HTTP/1.0' |
| $_SERVER['REQUEST_METHOD'] | ページにアクセスする際に使用されたリクエストのメソッド名です。 'GET', 'HEAD', 'POST', 'PUT' など。注意:リクエストのメソッドが HEAD だった場合、 PHP スクリプトはヘッダを送信した後（言い換えれば、 出力バッファリングを行わずに全出力を処理した後）に終了します。 |
| $_SERVER['REQUEST_TIME'] | リクエストの開始時のタイムスタンプ。PHP 5.1.0 以降で利用可能。 |
| $_SERVER['QUERY_STRING'] | ページがアクセスされた際にもし検索引数があればそれが格納されます。 |
| $_SERVER['DOCUMENT_ROOT'] | 現在実行されているスクリプトが存在するドキュメントルート ディレクトリです。サーバのコンフィグレーションファイルで 定義されています。 |
| $_SERVER['HTTP_ACCEPT'] | 現在のリクエストの Accept: ヘッダがもしあれば その内容。 |
| $_SERVER['HTTP_ACCEPT_CHARSET'] | 現在のリクエストの Accept-Charset: ヘッダが もしあればその内容。例: 'iso-8859-1,*,utf-8' |
| $_SERVER['HTTP_ACCEPT_ENCODING'] | 現在のリクエストに Accept-Encoding: ヘッダが もしあればその内容。例: 'gzip' |
| $_SERVER['HTTP_ACCEPT_LANGUAGE'] | 現在のリクエストに Accept-Language: ヘッダが もしあればその内容。例: 'en' |
| $_SERVER['HTTP_CONNECTION'] | 現在のリクエストに Connection: ヘッダが もしあればその内容。例: 'Keep-Alive' |
| $_SERVER['HTTP_HOST'] | 現在のリクエストに Host: ヘッダが もしあればその内容。 |
| $_SERVER['HTTP_REFERER'] | 現在のページに遷移する前にユーザエージェントが参照していた ページのアドレス（もしあれば）。これはユーザエージェントに よってセットされます。全てのユーザエージェントが これをセットしているわけではなく、また、HTTP_REFERER を変更する機能を持つものもああります。 要するに、信頼するべきものではありません。 |
| $_SERVER['HTTP_USER_AGENT'] | 現在のリクエストに User-Agent: ヘッダが もしあればその内容。ページにアクセスしてきているユーザエージェント のしるしの文字列です。典型的な例は、 Mozilla/4.5 [en] (X11; U; Linux 2.2.9 i586)。たとえば、 get_browser() でこの値を使って ページの出力をそのブラウザにあわせたものにすることも できるでしょう。 |
| $_SERVER['HTTPS'] | スクリプトが HTTPS プロトコルを通じて実行されている場合に 空でない値が設定されます。注意: ISAPI を IIS で使用している場合は、HTTPS プロトコルを通さないでリクエストが行われたときの値は off となることに注意しましょう。 |
| $_SERVER['REMOTE_ADDR'] | 現在ページをみているユーザの IP アドレス。 |
| $_SERVER['REMOTE_HOST'] | 現在のページにアクセスしているユーザーのホスト名。DNS の逆引き検索は ユーザの REMOTE_ADDR に基づいています。注意: Web サーバがこの値を生成できるように設定されている必要があります。 例えば Apache の場合 HostnameLookups On が httpd.conf に設定されていなければこの値は生成されません。 gethostbyaddr() もご覧ください。 |
| $_SERVER['REMOTE_PORT'] | ユーザのマシンから Web サーバへの通信に使用されているポート番号 |
| $_SERVER['SCRIPT_FILENAME'] | 現在実行されているスクリプトの絶対パス※注意:file.php あるいは ../file.php のような相対パスを指定して CLI でスクリプトが実行されている場合、 $_SERVER['SCRIPT_FILENAME'] には ユーザが指定した相対パスが含まれます。 |
| $_SERVER['SERVER_ADMIN'] | Web サーバの設定ファイルの SERVER_ADMIN (Apache の場合)ディレクティブ にセットされている値。スクリプトがバーチャルホスト上で 実行されている場合、バーチャルホストに対して値が定義されます。 |
| $_SERVER['SERVER_PORT'] | Web サーバの通信ポートとして使用されているポート番号。デフォルトでは '80' ですが、例えば SSL を使用している場合は セキュア HTTP ポートとして設定されている値に変わります。 |
| $_SERVER['SERVER_SIGNATURE'] | サーバ上で生成されたページに追加される、 サーバのバージョン名とバーチャルホスト名の文字列。 Web サーバの設定で有効になっていることが必要です。 |
| $_SERVER['PATH_TRANSLATED'] | バーチャルからリアルへのマッピングがなされた後の、 現在のスクリプトのファイルシステム上（ドキュメントルートではなく） でのパス。注意: PHP 4.3.2 以降、PATH_TRANSLATED は、 Apache 2 SAPI において暗黙のうちに設定されなく なりました。一方、Apache 1 では、この値が Apache により設定されない場合、 SCRIPT_FILENAME と同じ値に設定されます。 この変更は、PATH_TRANSLATED は PATH_INFO が定義されている場合のみ 存在するべきであるという CGI の規約を満たすために 行われました。 Apache 2 ユーザは、PATH_INFO を定義するために httpd.conf の中で AcceptPathInfo = On を使用することが可能です。 |
| $_SERVER['SCRIPT_NAME'] | 現在のスクリプトのパス。 スクリプト自身のページを指定するのに有用です。 __FILE__ 定数には、カレント(すなわち読み込まれた)ファイルのパスとファイル名が 含まれます。 |
| $_SERVER['REQUEST_URI'] | ページにアクセスするために指定された URI。例えば、 '/index.html' |
| $_SERVER['PHP_AUTH_DIGEST'] | HTTP ダイジェスト認証を 行っている場合、クライアントから送られた 'Authorization' ヘッダの 内容が設定されます（適切な認証処理を行うために利用します）。 |
| $_SERVER['PHP_AUTH_USER'] | HTTP 認証しているときにそのユーザ名がセットされます。 |
| $_SERVER['PHP_AUTH_PW'] | HTTP 認証しているときにそのユーザの パスワードがセットされます。 |
| $_SERVER['AUTH_TYPE'] | HTTP 認証しているときにその認証形式がセットされます。 |
| $_SERVER['PATH_INFO'] | 実際のスクリプトファイル名とクエリ文字列の間にある、クライアントが提供するパス名情報。 たとえば、現在のスクリプトに http://www.example.com/php/path_info.php/some/stuff?foo=bar という URL でアクセスしていた場合の $_SERVER['PATH_INFO'] は /some/stuff となります。 |
| $_SERVER['ORIG_PATH_INFO'] | PHP で処理される前の 'PATH_INFO' の原本。 |