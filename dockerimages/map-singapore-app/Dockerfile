# Create a dockerfile to build an apache web server for my management web portal
FROM httpd:2.4.66

COPY version.txt /tmp/version.txt
RUN APP_VERSION="$(cat /tmp/version.txt | tr -d '\n')"
COPY index.html /usr/local/apache2/htdocs/index.html
RUN sed -i "s/versionNumber/$APP_VERSION/g" /usr/local/apache2/htdocs/index.html
