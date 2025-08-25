# Book Tracker Application

A full-stack book tracking application with a Flutter frontend and ASP.NET Core backend, featuring user authentication, book management, reading progress tracking, and analytics dashboard.

## Default Login Information

The application automatically creates default users when first started:

### Desktop Admin Account
- **Email**: `admin@admin.com`
- **Password**: `password`
- **Role**: Administrator
- **Purpose**: Access to admin dashboard with user management and analytics

### Mobile User Account
- **Email**: `user@user.com`
- **Password**: `password`
- **Role**: Regular User
- **Purpose**: Standard user account for mobile/general use

Both accounts come pre-loaded with sample books and reading data for demonstration purposes.

## Features

- **Multi-platform Frontend**: Flutter app supporting desktop (Windows), mobile (Android/iOS), and web
- **Book Management**: Add, track, and manage your personal book library
- **Reading Progress**: Track reading status, current page, ratings, and reviews
- **Google Books Integration**: Real book data and cover images from Google Books API
- **Analytics Dashboard**: Admin panel with user statistics and reading metrics
- **Real-time Statistics**: RabbitMQ-powered statistics service
- **File Storage**: MinIO for profile pictures and file uploads

## Architecture

- **Backend**: ASP.NET Core 9.0 Web API
- **Frontend**: Flutter (multi-platform)
- **Database**: PostgreSQL
- **Message Queue**: RabbitMQ
- **File Storage**: MinIO
- **Statistics Service**: Dedicated microservice for analytics
- **Containerization**: Docker Compose for easy deployment

## Prerequisites

- [Docker](https://www.docker.com/get-started) and Docker Compose
- Android emulator (AVD) or physical Android device (for mobile testing)
- [Git](https://git-scm.com/) (for version control)

## Quick Start

### 1. Clone the Repository

```bash
git clone <your-repository-url>
```
### 1.1 Extract the Files

### 2. Start Backend Services

Navigate to the API directory and start all backend services:

```bash
cd BookTrackerAPI
docker compose up --build
```

This will start:
- PostgreSQL database
- RabbitMQ message queue
- MinIO file storage
- Book Tracker API
- Statistics Service

The API will be available at `http://localhost:8080`

### 3. Run the Frontend Applications

Pre-built applications are provided in the repository for easy setup:

**For Desktop (Windows):**
1. Navigate to the `desktop-fit-build-dd-mm--yy/Release/` folder
2. Double-click `book_tracker.exe` to run the desktop application

**For Mobile (Android):**
1. Start your Android emulator (AVD) or connect a physical Android device
2. Navigate to the `mobile-fit-build-dd-mm--yy/flutter-apk/` folder
3. Drag and drop the `book_tracker.apk` file onto your Android emulator
4. The app will automatically install and can be launched from the app drawer

## API Documentation

Once the backend is running, you can access:

- **Swagger UI**: `http://localhost:8080/swagger`
- **API Base URL**: `http://localhost:8080/api`

## Database Seeding

The application automatically seeds the database with:

- **Default Users**: Admin and regular user accounts
- **Sample Books**: 10 popular books with real data from Google Books API (with covers)
- **Test Data**: 15 additional test users with 15 sample books for analytics demonstration
- **User Books**: Sample reading progress data across different statuses (Want to Read, Reading, Completed)

## Configuration

### Backend Configuration

The main configuration is in `BookTrackerAPI/appsettings.json`:

### Frontend Configuration

The Flutter app configuration is in `book_tracker/lib/config.dart`:

## Development

### Backend Development

1. Navigate to `BookTrackerAPI`
2. Restore dependencies: `dotnet restore`
3. Run the API: `dotnet run`

### Frontend Applications

Pre-built applications are provided:
- **Windows Desktop**: `desktop-fit-build-dd-mm-yy/Release/book_tracker.exe`
- **Android Mobile**: `mobile-fit-build-dd-mm--yy/flutter-apk/book_tracker.apk`

For development or building from source, you'll need the Flutter SDK.

### Database Migrations

If you need to create new migrations:

```bash
cd BookTrackerAPI
dotnet ef migrations add <MigrationName>
dotnet ef database update
```

## Docker Services

The `docker-compose.yaml` includes:

- **PostgreSQL**: Database server (port 5433)
- **RabbitMQ**: Message queue with management UI (port 15672)
- **MinIO**: Object storage with console (port 9001)
- **Book Tracker API**: Main backend service (port 8080)
- **Statistics Service**: Analytics microservice

## Ports

- **API**: 8080
- **Database**: 5433
- **RabbitMQ**: 5672 (AMQP), 15672 (Management UI)
- **MinIO**: 9000 (API), 9001 (Console)
- **Flutter Web**: 3000 (if running web version)

## Troubleshooting

### Backend Issues

1. **Database Connection**: Ensure PostgreSQL container is running
2. **RabbitMQ Connection**: Check if RabbitMQ service is healthy
3. **Port Conflicts**: Make sure ports 5433, 5672, 8080, 9000 are available

### Frontend Issues

1. **API Connection**: Verify the backend is running on `http://localhost:8080`
2. **CORS Issues**: The backend is configured to allow localhost origins
3. **Flutter Issues**: Run `flutter doctor` to check Flutter installation

### Common Solutions

**Clear Docker containers and restart:**
```bash
cd BookTrackerAPI
docker compose down -v
docker compose up -d --build
```

**Re-install Android app:**
```bash
# If the APK doesn't install properly, try:
# 1. Uninstall the existing app from the emulator
# 2. Restart the emulator
# 3. Drag and drop the APK again
```
