FROM wordpress:5.3.2-php7.4-fpm

# Install wordpress to a different path
# other than the default /var/www/html
# ANNOYINGLY, the VOLUME /var/www/html created
# by parent image can not be removed
WORKDIR /var/www/wordpress

# Unzip is required to unzip the MDx Theme file
RUN set -eux; \
    apt-get update; \
    apt-get install -y --no-install-recommends \
        unzip \
    ; \
    rm -rf /var/lib/apt/lists/*

# INSTALLING MDX THEME
ENV MDX_VERSION V1.9.9
ENV MDX_SHA1 E5943591C0AF724690D418AB67715764F42BB205

RUN set -ex; \
    curl -o mdx.zip -fSL "https://github.com/yrccondor/mdx/releases/download/${MDX_VERSION}/mdx.zip"; \
    echo "$MDX_SHA1 *mdx.zip" | sha1sum -c -; \
    mkdir -p wp-content/themes; \
    unzip mdx.zip -d ./wp-content/themes; \
    rm mdx.zip; \
    # need test
    apt-get purge -y unzip

# Creating new volume to store data
VOLUME [ "/var/www/wordpress" ]
