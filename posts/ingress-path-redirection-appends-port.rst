.. title: Ingress path redirection appends port
.. slug: ingress-path-redirection-appends-port
.. date: 2020-12-08 02:29:14 UTC+03:00
.. tags: kubernetes, ingress
.. category: 
.. link: 
.. description: 
.. type: text

Ingress bazi URL isteklerine container port'u ile redirect etmeye calistigi gibi bir sorunla karsilasabilirsiniz. Ornek olarak biraz daha acmak gerekirse;

.. code:: bash

    $ curl -I http://cafe.example.com/coffee/

    HTTP/1.1 200 OK
    Date: Mon, 07 Dec 2020 23:47:21 GMT
    Content-Type: text/html
    Content-Length: 87466
    Connection: keep-alive
    Last-Modified: Mon, 07 Dec 2020 20:48:36 GMT
    ETag: "5fce9524-155aa"
    Accept-Ranges: bytes


Yukarida goruldugu "http://cafe.example.com/coffee/" adresine gonderdigimiz istek saglikli sekilde "200" kodunu cevap olarak donuyor.
Birde "http://cafe.example.com/coffee" seklinde istekte bulunarak test edelim:

.. code:: bash

    $ curl -I http://cafe.example.com/coffee

    HTTP/1.1 301 Moved Permanently
    Date: Sun, 07 Dec 2020 23:52:48 GMT
    Content-Type: text/html
    Content-Length: 169
    Connection: keep-alive
    Location: http://cafe.example.com:8080/coffee


Bu ornek ise goruldugu gibi "http://hostname:cointainer_port/paths" seklinde container portunu da ekleyerek sayfayi yanlis sekilde redirect etmeye calisiyor ve sayfa ulasilamaz oluyor.
Buradaki **'8080'** portu ingress'in arka tarafindaki nginx container'in yayin yapmakta olan portu.

Sorunun sebebine gelince, bu sorunun ingress ile hic bir alakasi yok. Hem **kubernetes/ingress-nginx** hem de **nginxinc/nginx-ingress** ingress controller'larinda nginx konfigurasyonu uzerindeki `port_in_redirect <http://nginx.org/en/docs/http/ngx_http_core_module.html#port_in_redirect>`_ degeri default olarak 'off' olarak.
Fakat arka tarafta calisan nginx container uzerindeki bu konfigurasyonu '*on*' yapilmissa bu durumla karsilasabilirsiniz. Bunu nginx.conf uzerinde '*port_in_redirect off;*' seklinde kapatarak yasanmasini engelleyebilirsiniz.

Asagidaki sekilde nginx.conf'u configmap'e ekleyerek nginx pod'un bu configmap'i kullanmasini saglayarak deployment yapabilirsiniz.

.. code:: yaml

    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: nginx-conf
    data:
      nginx.conf: |
        worker_processes  1;

        error_log  /var/log/nginx/error.log warn;
        pid        /tmp/nginx.pid;


        events {
            worker_connections  1024;
        }


        http {
            proxy_temp_path /tmp/proxy_temp;
            client_body_temp_path /tmp/client_temp;
            fastcgi_temp_path /tmp/fastcgi_temp;
            uwsgi_temp_path /tmp/uwsgi_temp;
            scgi_temp_path /tmp/scgi_temp;

            include       /etc/nginx/mime.types;
            default_type  application/octet-stream;

            log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                              '$status $body_bytes_sent "$http_referer" '
                              '"$http_user_agent" "$http_x_forwarded_for"';

            access_log  /var/log/nginx/access.log  main;

            sendfile        on;
            #tcp_nopush     on;

            port_in_redirect off;

            keepalive_timeout  65;

            #gzip  on;

            include /etc/nginx/conf.d/*.conf;
        }

    ---

    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: coffee
    spec:
      replicas: 3
      selector:
        matchLabels:
          app: coffee
      template:
        metadata:
          labels:
            app: coffee
        spec:
          containers:
          - name: www
            image: nginxinc/nginx-unprivileged
            ports:
            - containerPort: 8080
            volumeMounts:
            - name: nginx-conf
              mountPath: /etc/nginx/nginx.conf
              subPath: nginx.conf
              readOnly: true

    ---

    ---
    apiVersion: v1
    kind: Service
    metadata:
      name: coffee-svc
    spec:
      ports:
      - port: 80
        targetPort: 8080
        protocol: TCP
        name: http
      selector:
        app: coffee

