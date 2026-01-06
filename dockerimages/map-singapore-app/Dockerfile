# Create a dockerfile to build an apache web server for my management web portal
FROM httpd:2.4.66

COPY version.txt /tmp/version.txt
RUN echo "window.APP_VERSION = '$(cat /tmp/version.txt | tr -d '\n')';" > /usr/share/nginx/html/version.js
COPY index.html /usr/local/apache2/htdocs/index.html
