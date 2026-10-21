FROM jekyll/jekyll:pages AS build

WORKDIR /srv/jekyll
COPY . .
RUN jekyll build --verbose

FROM nginx:1.27-alpine AS runtime

COPY --from=build /srv/jekyll/_site /usr/share/nginx/html
EXPOSE 80
