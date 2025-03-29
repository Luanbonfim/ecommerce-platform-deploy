# E-commerce Platform

A full-stack e-commerce platform built with Angular (frontend) and ASP.NET (backend).
![image](https://github.com/user-attachments/assets/d157419d-37a0-4ae0-bcdd-0bda2348c745)
![image](https://github.com/user-attachments/assets/b5f18bf0-baf8-4d22-a5d5-8a9522885f77)

## Prerequisites

- Docker Desktop
- Git

## Project Structure

```
.
├── ecommerce-platform-app/    # Angular frontend (submodule)
├── Products-ASP.NET/          # ASP.NET Core backend (submodule)
│   ├── certs/                 # SSL certificates
│   └── data/                  # SQLite database
├── docker-compose.yml         # Docker Compose configuration
├── .env.example              # Template for environment variables
└── README.md                 # This file
```

## Setup Instructions

1. Clone the repository with submodules:
```bash
# Clone the repository with submodules
git clone --recursive https://github.com/Luanbonfim/ecommerce-platform-deploy.git

# If you've already cloned without submodules, run:
git submodule init
git submodule update
```

2. Set up environment variables:
   - Copy `.env.example` to `.env`:
     ```bash
     cp .env.example .env
     ```
   - Update the following variables in `.env`:
     ```env
     # Get these from Google Cloud Console (https://console.cloud.google.com)
     GOOGLE_CLIENT_ID=your_google_client_id_here
     GOOGLE_CLIENT_SECRET=your_google_client_secret_here

     # Default values - can be changed in docker-compose.yml
     CERTIFICATE_PATH=your certificate path
     CERTIFICATE_PASSWORD=your certificate password
     ```

3. Ensure you have the SSL certificate:
   - Place your `api_cert.pfx` file in the `your certificate path` directory


## Running the Application

1. Build and start all services:
```bash
docker-compose up --build
```

2. Access the applications:
   - Frontend: https://localhost:4200
   - Backend API: https://localhost:7263

## Development

### Frontend (Angular)
- Located in `ecommerce-platform-app/`
- Built with Angular
- Uses SSL for secure connections
- Environment variables are injected during build

### Backend (ASP.NET Core)
- Located in `Products-ASP.NET/`
- RESTful API with authentication
- Uses SQLite database
- SSL certificate for HTTPS

## Environment Variables

Required environment variables in `.env`:

### Google OAuth Configuration
- `GOOGLE_CLIENT_ID`: Your Google OAuth client ID
  - Get this from Google Cloud Console
  - Required for authentication
- `GOOGLE_CLIENT_SECRET`: Your Google OAuth client secret
  - Get this from Google Cloud Console
  - Required for authentication

### SSL Certificate Configuration
- `CERTIFICATE_PATH`: Path to the SSL certificate
  - example: `/certs/api_cert.pfx`
  - Can be changed in docker-compose.yml
- `CERTIFICATE_PASSWORD`: Password for the SSL certificate
  - example: `123456`
  - Can be changed in docker-compose.yml

### Database Configuration
- `ConnectionStrings__DefaultConnection`: SQLite database path
  - Default: `Data Source=/app/data/Products.db`
  - Used by the backend service

### Frontend Configuration
- `NODE_ENV`: Environment mode
  - Default: `development`
- `PORT`: Frontend port
  - Default: `4200`

## Database

The application uses SQLite as its database:
- Database file is stored in `Products-ASP.NET/data/`
- Persisted using Docker volumes
- Automatically initialized on first run

## Working with Git Submodules

### Updating Submodules
```bash
# Update all submodules to their latest commits
git submodule update --remote

# Update a specific submodule
git submodule update --remote Products-ASP.NET
```

### Making Changes in Submodules
1. Navigate to the submodule directory:
   ```bash
   cd Products-ASP.NET  # or ecommerce-platform-app
   ```
2. Make your changes
3. Commit and push changes in the submodule
4. Return to the main repository and commit the submodule reference:
   ```bash
   cd ..
   git add Products-ASP.NET  # or ecommerce-platform-app
   git commit -m "Update submodule to latest version"
   git push
   ```

### Pulling Changes
```bash
# Pull changes from the main repository
git pull

# Update submodules after pulling
git submodule update --init --recursive
```

## Troubleshooting

1. If you encounter SSL certificate issues:
   - Verify the certificate is in the correct location
   - Check the certificate password in docker-compose.yml
   - Ensure the certificate is valid and not expired

2. If the database is not persisting:
   - Check if the data directory exists
   - Verify Docker volume permissions

3. If services fail to start:
   - Check Docker logs: `docker-compose logs`
   - Verify all environment variables are set
   - Ensure ports 4200 and 7263 are available

4. If submodules are not updating:
   - Run `git submodule init` followed by `git submodule update`
   - Check if you have access to the submodule repositories
   - Verify the submodule URLs in `.gitmodules`

## Stopping the Application

To stop all services:
```bash
docker-compose down
```

To stop and remove all data (including the database):
```bash
docker-compose down -v
```

## Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a new Pull Request

## License

[Your License Here] 
