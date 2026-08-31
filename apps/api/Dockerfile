# Development image for apps/api.
# Provides the Rails toolchain so the application can be generated later
# without installing Ruby or Rails on the host.

FROM ruby:3.3.6-bookworm

RUN apt-get update -qq && \
    apt-get install -y --no-install-recommends \
      build-essential \
      git \
      libpq-dev \
      libyaml-dev \
      postgresql-client \
    && rm -rf /var/lib/apt/lists/*

ARG UID=1000
ARG GID=1000

RUN groupadd --gid "${GID}" app && \
    useradd --uid "${UID}" --gid app --create-home --shell /bin/bash app && \
    mkdir -p /app && \
    chown -R app:app /usr/local/bundle /app

USER app
WORKDIR /app

# Matches the planned apps/api scaffold (Ruby 3.3.6 / Rails 8.1).
RUN gem install rails -v "~> 8.1.0" --no-document

EXPOSE 3000

# No Rails app yet. Keep the container running so Compose stays up and
# engineers can exec into it (generation is a later increment).
CMD ["sleep", "infinity"]
