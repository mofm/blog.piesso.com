.. title: Locust: Load Testing Tool
.. slug: locust-load-testing-tool
.. date: 2017-12-04 00:37:28 UTC+03:00
.. tags: locust, loadtesting, tools 
.. category: 
.. link: 
.. description: 
.. type: text


*Locust*, kullanimi diger uygulamalara gore kolay distributed load testing aracidir. Websitenizi ya da diger sistemlerinizi kullanici sayilarini simule ederek yazdiginiz kodlari ya da sistemlerinizi load testing yaparak kontrol etmenize olanak saglar.

**Locust'un ozellikleri:**

* Kolay test senaryosu yazma. Diger araclara gore daha sade ve kolay syntax ile yazabilme. Python'a asina olanlar icin yabancilik cekmeyecekleri sekilde python kod.

* Distributed load testing. Tekil ya da coklu makinelerle load testing yapabilme. Ister kullandiginiz bir bilgisayarla isterse 20 makine ile test yapabilme imkani.

* Webarayuzu. Locust HTML+JS ile size realtime test sonuclarini webarayuzunden izleyebilme imkani sagliyor.

* Her turlu sistemi test edebilirsiniz. Sadece websitelerini degil ldap,smtp gibi servis verdiginiz her turlu sistemleri biraz python biliyorsaniz client kod vs yazayarak test edebilirsiniz.

* Apache JMeter gibi java bagimliliginiz kalmadan bu testlerinizi yapabilirsiniz.( JMeter uzerinde SSL sertifikaniz 4096 bit gibi yuksek sifrelenmis ise javanin en yuksek 2048 bit desteklemesi yuzunden basarili olamayabilirsiniz. )

**Kurulumu**

Locust, Python 2.7, 3.3, 3.4, 3.5,3.6. versiyonlarini desteklemektedir. Sistemizdeki 'pip' kurulu oldugundan emin olun. Bir cok modern sistemlerde halihazirda kurulu olarak zaten geliyor.

.. code:: bash

   # pip install locustio

Eger sadece kendi kullaniciniz icin kuracaksaniz;

.. code:: bash

   $ pip install --user locustio

Ardindan '~/.local/bin/' dizinini "PATH'inize ekleyin. GNU/Linux dagitiminiza ya da sisteminize gore '.bashrc' ya da 'bash_profile' dosyaniza eklemeniz gerekir.

.. code:: bash

   PATH=$PATH:~/.local/bin

Kurulum adimlari bu kadar. 

.. note:: Son olarak not dusmek gerekir. Eger load testing yaparken yuksek sayida kullanici ile senaryo gerceklestirecekseniz sistemiz ve load-testing yapan kullaniciniz icin file-limit degerlerini yukseltmeniz gerekebilir.

Ilk olarak sistemiz uzerinden file-limit degerini ogrenip yukseltmek icin;

.. code:: bash

   # cat /proc/sys/fs/file-max
   75000

Yukarda goruldugu gibi sistem uzerinde file-limit degeri '75000'. Bu degeri ornek olarak '750000' yukseltmek icin;

.. code:: bash

   # sysctl -w fs.file-max=750000

Sistem uzerinde kalici olarak degistirmek icin, "/etc/sysctl.conf" dosyasina asagidaki satiri ekleyin.

.. code:: bash

   fs.file-max = 750000

Aktif etmek icin;

.. code:: bash

   # sysctl -p

Bu limit degerlerini sisteme giris yaptiginiz ya da test yapacaginiz kullanici icin yukseltmek icin '/etc/security/limits.conf' dosyaniza asagidaki gibi degerleri ekleyin;

.. code:: bash

   ## hard limit 
   kullanici1        hard nofile 10000
   ## soft limit
   kullanici1        soft nofile 5000

Yaptiginiz degisikligin aktif olmasi icin cikis yapip tekrar giris yapmaniz gereklidir.


**Senaryo olusturma**

Locust icin cesitli senaryolar yazabilirsiniz. Iki basit ornek verelim.

*Ornek 1:* Websitenizin anasayfasini ve hakkimda sayfalarini test etmek icin load-testing senaryosu yazalim.

.. code:: python

   from locust import HttpLocust, TaskSet, task

   class MyTaskSet(TaskSet):
        @task(2)
        def index(self):
                self.client.get("/")

        @task(1)
        def about(self):
                self.client.get("/hakkinda/")

   class MyLocust(HttpLocust):
        task_set = MyTaskSet
        min_wait = 5000
        max_wait = 15000

'min_wait' ve 'max_wait' degerleri simule eden kullanicilarin bu sureler arasinda istek yapmasini gosterir.

*Ornek 2:* Websitenizin login sayfasina kullanici ile giris yapip, anasayfasini ve profile sayfasini test senaryosu yazalim.

.. code:: python

   from locust import HttpLocust, TaskSet
   
   def login(l):
        l.client.post("/login", {"username":"ellen_key", "password":"education"})

   def index(l):
        l.client.get("/")

   def profile(l):
        l.client.get("/profile")

   class UserBehavior(TaskSet):
        tasks = {index: 2, profile: 1}
        
        def on_start(self):
                login(self)
   
   class WebsiteUser(HttpLocust):
        task_set = UserBehavior
        min_wait = 5000
        max_wait = 9000

**Load-Testing Yapmak**

Locust ile yazdigimiz senaryolar ile load-testing yapmak icin;

.. code:: bash

   $ locust --host=http://example.com

ya da yazdigimiz senaryo dosyasinin yolunu belirterek;

.. code:: bash

   $ locust -f locust_files/my_locust_file.py --host=http://example.com

Test basladiktan sonra tarayiciniza 'localhost:8089' yazarak kullanicilari simule edip testinizi izleyebilirsiniz.
