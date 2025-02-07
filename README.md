# Project Setup and Usage Guide

A [Docker](https://www.docker.com/)-based installer and runtime for the [Symfony](https://symfony.com) web framework,
with [FrankenPHP](https://frankenphp.dev)!

![CI](https://github.com/dunglas/symfony-docker/workflows/CI/badge.svg)

## Getting Started

1. If not already done, [install Docker Compose](https://docs.docker.com/compose/install/) (v2.10+)
2. Run `docker compose build --no-cache` to build fresh images
3. Run `docker compose up --pull always -d --wait` to set up and start a fresh Symfony project
4. Open `https://localhost` in your favorite web browser and [accept the auto-generated TLS certificate](https://stackoverflow.com/a/15076602/1352334)
5. Run `docker compose down --remove-orphans` to stop the Docker containers.
## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Database Setup](#database-setup)
- [Running the Application](#running-the-application)
- [Running Tests](#running-tests)
- [Building and Managing Frontend Assets](#building-and-managing-frontend-assets)
- [Additional Commands and Troubleshooting](#additional-commands-and-troubleshooting)
- [Deployment](#deployment)
- [Contributing](#contributing)
- [License](#license)

## Prerequisites

Before setting up the project, ensure you have the following installed:

- **PHP (>=8.0)**: The backend is built with Symfony, which requires PHP 8.0 or later.
- **Composer**: A dependency manager for PHP.
- **Symfony CLI**: Helps manage Symfony applications.
- **Node.js & npm**: Required for frontend dependencies and asset compilation.
- **Docker & Docker Compose** (if using containerized services): Recommended for a consistent environment setup.

## Installation

1. **Clone the repository:**

   ```sh
   git clone <repository-url>
   cd Symfony-Framework
   ```

2. **Install PHP dependencies:**

   ```sh
   composer install
   ```

3. **Install Node.js dependencies:**

   ```sh
   npm install
   ```

4. **Configure environment variables:**

   - Copy the `.env.dev` file to `.env`:
     ```sh
     cp .env.dev .env
     ```
   - Open `.env` and configure database credentials, API keys, and other required settings.

## Database Setup

1. **Run database migrations:**

   ```sh
   php bin/console doctrine:migrations:migrate
   ```

2. **If using fixtures, load sample data:**

   ```sh
   php bin/console doctrine:fixtures:load
   ```

## Running the Application

### Running Locally with Symfony CLI

Start the Symfony development server:

```sh
symfony serve
```

This will start the application and make it accessible at `http://127.0.0.1:8000/`.

### Running with Docker (if applicable)

Ensure that Docker is installed and running on your system. Then, start the application with:

```sh
docker-compose up --build -d
```

This command builds the Docker images (if not already built) and runs the application in detached mode.

## Running Tests

Run the PHPUnit test suite to verify the functionality:

```sh
php bin/phpunit
```

Ensure that database migrations are applied before running the tests.

## Building and Managing Frontend Assets

1. **Compile and watch frontend assets:**

   ```sh
   npm run dev
   ```

2. **Build assets for production:**

   ```sh
   npm run build
   ```

3. **Run the Webpack development server (if applicable):**

   ```sh
   npm run start
   ```

## Additional Commands and Troubleshooting

- **Clear the application cache:**
  ```sh
  php bin/console cache:clear
  ```
- **Check for security vulnerabilities:**
  ```sh
  symfony check:security
  ```
- **Verify environment settings:**
  ```sh
  symfony dotenv:debug
  ```

## Deployment

For deploying the project to production:

1. Ensure all dependencies are installed:
   ```sh
   composer install --no-dev --optimize-autoloader
   npm install && npm run build
   ```
2. Apply database migrations:
   ```sh
   php bin/console doctrine:migrations:migrate --no-interaction
   ```
3. Clear and warm up the cache:
   ```sh
   php bin/console cache:clear --env=prod --no-debug
   ```
4. Restart the web server if necessary.

## Contributing

Contributions are welcome! To contribute, follow these steps:

1. Fork the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Make your changes and commit them (`git commit -m 'Add new feature'`).
4. Push to the branch (`git push origin feature-branch`).
5. Open a Pull Request.

## License

This project is licensed under the MIT License.

## Contact

For any issues, feel free to open an issue or contact the maintainers via GitHub.

