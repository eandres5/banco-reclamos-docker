FROM nginx:1.27-alpine

RUN rm -rf /usr/share/nginx/html/*
RUN rm /etc/nginx/conf.d/default.conf

COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY dist/app-reclamos/browser/ /usr/share/nginx/html/app-reclamos/

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]