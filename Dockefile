# Use an official Ubuntu base image
FROM ubuntu:20.04

# Set environment variables to avoid interactive prompts during package installation
ENV DEBIAN_FRONTEND=noninteractive

# Update the package list and install dependencies
RUN apt-get update && \
    apt-get install -y \
    curl \
    git \
    docker.io \
    docker-compose \
    php \
    php-cli \
    php-fpm \
    php-mbstring \
    php-xml \
    php-curl \
    php-json \
    php-mysql \
    && apt-get clean

# Install any other dependencies needed by the docker-pterodactyl-panel repository

# Clone the repository
RUN git clone https://github.com/YoshiWalsh/docker-pterodactyl-panel /docker-pterodactyl-panel

# Set working directory to the cloned repo
WORKDIR /docker-pterodactyl-panel

# Run Docker Compose and related commands
# Note: This will not actually work in the build phase since `docker-compose` needs to be run in a running Docker environment
# We will prepare the setup but not execute Docker Compose here. You'd have to run docker-compose after building the image.
RUN docker-compose pull  # Pull the required images

# You can create a custom entrypoint to run `php artisan` commands later
CMD ["sh", "-c", "sleep 5 && docker-compose up -d && docker exec -it docker-pterodactyl-panel_php-fpm_1 php artisan p:user:make"]
