ARG NODE_IMAGE=node:18-alpine
FROM ${NODE_IMAGE}
ARG VERSION

# Сохраняем метаданные
LABEL shadowbox.node_version=18.x
LABEL shadowbox.github.release=${VERSION}

STOPSIGNAL SIGKILL

# Установим системные зависимости
RUN apk add --no-cache --upgrade coreutils curl bash

# Копируем исходники
COPY . /opt/outline-server
WORKDIR /opt/outline-server

# Установим зависимости Node и соберём проект
RUN yarn install --frozen-lockfile && yarn build

# Обновление базы GeoIP
RUN /src/shadowbox/scripts/update_mmdb.sh

# Запуск Shadowbox
CMD ["/src/shadowbox/docker/cmd.sh"]
