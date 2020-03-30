# odoo13
git clone https://github.com/fdonadio1979/odoo13.git

git clone https://github.com/ingadhoc/docker-odoo.git


cd odoo13/

sudo cp Dockerfile ../docker-odoo

cd /docker-odoo

sudo docker build -t img_odoo_13 .

cd ../odoo13/

sudo docker-compose up -d

Bueno, el primer paso es tener instalado Odoo e instalar el módulo account (el módulo de contabilidad) junto con el módulo l10n_ar. Esto instala la localizcaión argentina que viene por defecto en Odoo. Luego tienen (en ajustes de la contabilidad) seleccionar el plan contable de responsables inscritos en Argentina. Habiendo hecho esto, uno puede configurar los datos de la empresa.


sudo docker exec -it -u 0 odoo13_web_1 bash

cd /home/odoo/src/repositories

git clone git clone https://github.com/ctmil/odoo-argentina -b 13.0


sudo apt-get install libssl-dev swig python3-dev gcc

sudo pip install m2crypto


sudo apt-get install make


sudo apt-get remove openssl


wget https://www.openssl.org/source/openssl-1.1.0e.tar.gz

tar xzvf openssl-1.1.0e.tar.gz

cd openssl-1.1.0e

./config -Wl,--enable-new-dtags,-rpath,'$(LIBRPATH)'

make

sudo make install


To verify it is working:

openssl version

  OpenSSL 1.1.0  25 Aug 2016
  

cd /home/odoo/src/repositories/odoo-argentina

sudo pip install -r requirements.txt


exit


sudo docker restart odoo13_web_1


sudo docker exec -it -u 0 odoo13_web_1 bash



Si hicieron esto exitosamente, el paso siguiente es en Odoo actualizar la lista de módulos; e instalar los siguientes módulos: account_payment_group, account_check y l10n_ar_afipws_fe. Esto instala las funcionalidades de recibos, cheques y factura electrónica. 


Bien, los pasos que quedan son configurar los certificados de la empresa; configurar los grupos de impuestos de la empresa (se necesita que el IVA 21%, IVA 10.5% e IVA Exento pertenezcan a un grupo de impuestos que sea de tipo IVA), y configurar el resto de los diarios para que funcione la factura electrónica. Pero son temas más propios de la configuración del sistema. Ya con esto debería funcionar el sistema, pero recuerden que aun esta en testeo la localización. No sean tan kamikazes de ponerla en producción sin haber probado.


# Referencias
https://www.moldeointeractive.com.ar/en_US/blog/moldeo-interactive-1/post/instructivo-para-instalacion-de-localizacion-argentina-para-odoo-13-community-741

https://odoo-usuario-inicial.readthedocs.io/es/latest/instalacion/odoo-13-ce/odoo-13-ce.html

https://forums.servethehome.com/index.php?resources/installing-openssl-1-1-0-on-ubuntu.21/

The problem was caused by openssl versions

https://stackoverflow.com/questions/58011032/docker-python-requests-results-in-dh-key-too-small-error
