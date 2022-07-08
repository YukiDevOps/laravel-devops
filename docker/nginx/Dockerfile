FROM nginx:1.23.0-alpine

# 設定ファイルを指定の場所に置く
COPY ./docker/nginx/server.conf /etc/nginx/nginx.conf


CMD ["nginx", "-g", "daemon off;"]
