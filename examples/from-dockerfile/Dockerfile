FROM ubi8/ruby-27

ADD app-src ./

# Workaround for https://github.com/sclorg/s2i-ruby-container/issues/469
# Only apply the config for the offending bundler version.
RUN (bundler --version | grep -vq 'Bundler version 2.3.26') || \
    bundle config set force_ruby_platform true

RUN bundle install --path ./bundle

CMD exec bundle exec "rackup -P /tmp/rack.pid --host 0.0.0.0 --port 8080"
