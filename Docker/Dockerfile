FROM centos:7
#installing required packages 
RUN yum install apr-util-devel gcc pcre-devel libxml2-devel wget curl gcc-devel curl-devel httpd-devel make -y 

WORKDIR /root
#installing httpd service 
RUN wget  https://www-eu.apache.org/dist//httpd/httpd-2.4.53.tar.gz &&\
              tar -xvxf httpd-2.4.53.tar.gz &&\
              rm -rf httpd-2.4.53.tar.gz &&\
              cd httpd-2.4.53 &&\
              ./configure && make clean && make && make install

#installing php7

RUN wget https://www.php.net/distributions/php-7.4.28.tar.gz &&\
    tar -xvzf php-7.4.28.tar.gz &&\
    rm -rf php-7.4.28.tar.gz &&\
    cd php-7.4.28 && ./configure --with-apxs2=/usr/local/apache2/bin/apxs --enable-mbstring --enable-mysqlnd --with-mysqli && make clean && make && make install 
COPY ./httpd.conf /usr/local/apache2/conf/httpd.conf

#installing WIKIMEDIA

RUN wget https://releases.wikimedia.org/mediawiki/1.37/mediawiki-1.37.1.tar.gz &&\
    tar -xvzf mediawiki-1.37.1.tar.gz &&\
    rm -rf mediawiki-1.37.1.tar.gz &&\
    mv mediawiki-1.37.1 /usr/local/apache2/htdocs/ &&\
    mv /usr/local/apache2/htdocs/mediawiki-1.37.1 /usr/local/apache2/htdocs/wiki

CMD /usr/local/apache2/bin/apachectl -DFOREGROUND
EXPOSE 80
