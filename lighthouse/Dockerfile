FROM quipper/circleci-base

USER root

# Install Google Chrome
# Based on https://github.com/SeleniumHQ/docker-selenium/blob/master/NodeChrome/Dockerfile
ARG CHROME_VERSION="google-chrome-stable"
RUN curl https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
  && echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list \
  && apt-get -y update \
  && apt-get -y install \
    ${CHROME_VERSION:-google-chrome-stable} \
  && rm /etc/apt/sources.list.d/google-chrome.list \
  && rm -rf /var/lib/apt/lists/* /var/cache/apt/*

USER quipper

# Install nvm and NodeJS and yarn
# - https://github.com/creationix/nvm#installation
ENV NODE_VERSION 6.11.1
RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.6/install.sh | bash \
  && echo 'export NVM_DIR="$HOME/.nvm"\n[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"' >> ~/.bash_profile \
  && /bin/bash -lc 'nvm --version' \
  && /bin/bash -lc 'nvm install $NODE_VERSION' \
  && /bin/bash -lc 'node --version'

# Install yarn
# - https://yarnpkg.com/lang/en/docs/install/#alternatives-tab
ENV YARN_VERSION 1.3.2
RUN /bin/bash -lc 'curl -o- -L https://yarnpkg.com/install.sh | bash -s -- --version $YARN_VERSION' \
  && echo 'PATH="$PATH:$HOME/.yarn/bin"' >> ~/.bash_profile \
  && /bin/bash -lc 'yarn --version'

# Install Lighthouse
RUN /bin/bash -lc 'yarn global add lighthouse'
# Set environment variables required by Lighthouse
ENV CHROME_PATH "/usr/bin/google-chrome-stable"
ENV DISPLAY ":99.0"

# Install @google-cloud/bigquery for sending Lighthouse reports to BigQuery
RUN /bin/bash -lc 'yarn global add @google-cloud/bigquery'

# Set BASH_ENV to recognize CircleCI to .bash_profile
# https://discuss.circleci.com/t/how-to-add-a-path-to-path-in-circle-2-0/11554/4
ENV BASH_ENV '~/.bash_profile'