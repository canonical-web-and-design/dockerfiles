# Docker image to run maas in demoservice
FROM canonicalwebteam/dev:latest

# Install dependencies
RUN apt-get update
RUN apt-get -y install sudo libpq-dev python3-dev lsb-release

# Create a maas user.
RUN groupadd -r maas
RUN useradd -g maas -d /home/maas -s /sbin/nologin maas
RUN echo 'maas ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

# Swap to the maas user
USER maas

# Swap to the maas home folder and give ownership
WORKDIR /home/maas
COPY . .
RUN sudo chown -R maas:maas /home/maas

# Build Maas
RUN make install-dependencies
RUN make
RUN make syncdb
RUN make sampledata

CMD ["make", "run"]
