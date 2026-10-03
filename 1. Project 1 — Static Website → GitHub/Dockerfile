FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html
COPY style.css /usr/share/nginx/html/style.css

# Automate granting read/execute permissions to Nginx files
RUN chmod -R 755 /usr/share/nginx/html

EXPOSE 80