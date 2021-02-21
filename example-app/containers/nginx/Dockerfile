FROM nginx:1.19.7

LABEL maintainer="Johan Frank"

WORKDIR "/application"

ARG WWWGROUP
ARG WWWUSER

# Add user to group
RUN groupadd --force -g $WWWGROUP wessla
RUN useradd -ms /bin/bash --no-user-group -g $WWWGROUP -u $WWWUSER wessla

EXPOSE 80
