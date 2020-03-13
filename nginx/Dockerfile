FROM debian:jessie

MAINTAINER Maxence POUTORD <maxence.poutord@gmail.com>

RUN apt-get update && apt-get install -y \
    nginx mc nano

#ADD nginx.conf /etc/nginx/
#ADD deepmetrics.conf /etc/nginx/sites-available/
#ADD nlotv.conf /etc/nginx/sites-available/
#ADD vogue.conf /etc/nginx/sites-available/
#ADD indigotv.conf /etc/nginx/sites-available/
#ADD videomanager.conf /etc/nginx/sites-available/
#ADD ukraine.conf /etc/nginx/sites-available/
#ADD segodnya_hp.conf /etc/nginx/sites-available/

#RUN ln -s /etc/nginx/sites-available/deepmetrics.conf /etc/nginx/sites-enabled/deepmetrics.conf
#RUN ln -s /etc/nginx/sites-available/nlotv.conf /etc/nginx/sites-enabled/nlotv.conf
#RUN ln -s /etc/nginx/sites-available/vogue.conf /etc/nginx/sites-enabled/vogue.conf
#RUN ln -s /etc/nginx/sites-available/indigotv.conf /etc/nginx/sites-enabled/indigotv.conf
#RUN ln -s /etc/nginx/sites-available/videomanager.conf /etc/nginx/sites-enabled/videomanager.conf
#RUN ln -s /etc/nginx/sites-available/ukraine.conf /etc/nginx/sites-enabled/ukraine.conf
#RUN ln -s /etc/nginx/sites-available/segodnya_hp.conf /etc/nginx/sites-enabled/segodnya_hp.conf

RUN rm /etc/nginx/sites-enabled/default

#RUN echo "upstream php-upstream { server php:9000; }" > /etc/nginx/conf.d/upstream.conf

RUN usermod -u 1000 www-data

CMD ["nginx"]

EXPOSE 80
EXPOSE 443
