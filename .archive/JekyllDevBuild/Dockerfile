FROM ruby:3.1.1-alpine3.15

RUN apk add --no-cache build-base gcc bash cmake git nodejs-current

# install both bundler 1.x and 2.x incase you're running
# old gem files
# https://bundler.io/guides/bundler_2_upgrade.html#faq
RUN gem install bundler -v "~>1.0" && gem install bundler jekyll

EXPOSE 4000

WORKDIR /site

ENTRYPOINT [ "jekyll" ]

CMD [ "--help" ]


FROM jekyll as jekyll-serve

COPY docker-entrypoint.sh /usr/local/bin/

# on every container start, check if Gemfile exists and warn if it's missing
ENTRYPOINT [ "docker-entrypoint.sh" ]

CMD bundle exec jekyll serve -H 0.0.0.0 -P 4000 --trace --force_polling --livereload
