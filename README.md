# E-commerce Platform

A full-stack e-commerce platform built with Angular (frontend) and ASP.NET Core (backend).

## Prerequisites

- Docker Desktop
- Git

## Project Structure

```
.
├── ecommerce-platform-app/    # Angular frontend
├── Products-ASP.NET/          # ASP.NET Core backend
│   ├── certs/                 # SSL certificates
│   └── data/                  # SQLite database
├── docker-compose.yml         # Docker Compose configuration
├── .env.example              # Template for environment variables
└── README.md                 # This file
```

## Setup Instructions

1. Clone the repository:
```bash
git clone <repository-url>
cd ecommerce-platform
```

2. Create a `.env` file in the root directory with the following variables:
```env
GOOGLE_CLIENT_ID=your_google_client_id_here
GOOGLE_CLIENT_SECRET=your_google_client_secret_here
```

3. Ensure you have the SSL certificate:
   - Place your `api_cert.pfx` file in the `Products-ASP.NET/certs/` directory
   - The default certificate password is `123456` (can be changed in docker-compose.yml)

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

Required environment variables:
- `GOOGLE_CLIENT_ID`: Your Google OAuth client ID
- `GOOGLE_CLIENT_SECRET`: Your Google OAuth client secret
- `CERTIFICATE_PATH`: Path to the SSL certificate (default: /certs/api_cert.pfx)
- `CERTIFICATE_PASSWORD`: Password for the SSL certificate (default: 123456)

## Database

The application uses SQLite as its database:
- Database file is stored in `Products-ASP.NET/data/`
- Persisted using Docker volumes
- Automatically initialized on first run

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