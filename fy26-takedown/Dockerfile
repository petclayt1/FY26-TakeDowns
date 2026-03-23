# Static site for DigitalOcean App Platform / Droplets / any Docker host.
# HTTP port 8080 matches DO App Platform default for web services.
FROM nginx:1.27-alpine

COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY index.html /usr/share/nginx/html/index.html

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
