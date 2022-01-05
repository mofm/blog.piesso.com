.. title: Unbound DoH behind Nginx
.. slug: unbound-doh-behind-nginx
.. date: 2021-12-18 01:53:49 UTC+03:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text

Unbound DoH is waiting HTTP/2 requests. But Nginx proxy module doesn't support HTTP/2 on the upstream connections. 
So you can use grpc proxy:


.. code-block:: bash


   location /dns-query {
        grpc_pass grpc://unbound-host;
   }


and disable TLS for DNS-over-HTTP downstream service in unbound.conf:


.. code-block:: bash


   http-notls-downstream: yes
