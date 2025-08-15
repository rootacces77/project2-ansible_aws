FROM httpd:2.4

RUN apt-get update && apt-get upgrade -y 
RUN apt-get install libapache2-mod-evasive -y
RUN apt-get install -y libapache2-mod-security2
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN sed -i 's/Include conf\/extra\/proxy-html.conf/#Include conf\/extra\/proxy-html.conf/' /usr/local/apache2/conf/httpd.conf
RUN sed -i 's/#Include conf\/extra\/httpd-autoindex.conf/Include conf\/extra\/httpd-autoindex.conf/' /usr/local/apache2/conf/httpd.conf

RUN echo "LoadModule security2_module /usr/lib/apache2/modules/mod_security2.so" > /usr/local/apache2/conf/mod_security.conf && \
    echo "Include conf/mod_security.conf" >> /usr/local/apache2/conf/httpd.conf

RUN echo "LoadModule evasive20_module /usr/lib/apache2/modules/mod_evasive20.so" > /usr/local/apache2/conf/mod_evasive.conf && \
    echo "<IfModule mod_evasive20.c>" >> /usr/local/apache2/conf/mod_evasive.conf && \
    echo "  DOSHashTableSize    3097" >> /usr/local/apache2/conf/mod_evasive.conf && \
    echo "  DOSPageCount        2" >> /usr/local/apache2/conf/mod_evasive.conf && \
    echo "  DOSSiteCount        50" >> /usr/local/apache2/conf/mod_evasive.conf && \
    echo "  DOSPageInterval     1" >> /usr/local/apache2/conf/mod_evasive.conf && \
    echo "  DOSSiteInterval     1" >> /usr/local/apache2/conf/mod_evasive.conf && \
    echo "  DOSBlockingPeriod   10" >> /usr/local/apache2/conf/mod_evasive.conf && \
    echo "  DOSLogDir           \"/var/log/apache2/mod_evasive\"" >> /usr/local/apache2/conf/mod_evasive.conf && \
    echo "</IfModule>" >> /usr/local/apache2/conf/mod_evasive.conf && \
    echo "Include conf/mod_evasive.conf" >> /usr/local/apache2/conf/httpd.conf


EXPOSE 80/tcp
