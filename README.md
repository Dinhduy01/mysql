# MySQL Tutor Database on Render

This repository contains a MySQL database for a tutoring application that can be deployed on Render.

* Uses MySQL 8.0.24 via the [official MySQL Docker image](https://hub.docker.com/r/mysql/mysql-server)
* Configured with [Render Disks](https://render.com/docs/disks) for fast, persistent SSD storage
* Runs in a [private network](https://render.com/docs/private-services) for security

## Database Structure

This MySQL instance contains a tutoring application database with tables for:
- Users and authentication
- Classes and enrollment
- Blogs and comments
- Assignments and submissions
- Feedback and communication

## Deployment Instructions

1. Fork this repository to your GitHub account
2. Go to [Render Dashboard](https://dashboard.render.com/)
3. Create a new "Blueprint" instance
4. Connect your GitHub account and select this repository
5. Render will automatically deploy the MySQL database using the settings in `render.yaml`
6. The database will be accessible via the internal URL `mysql:3306` to other services on your Render account

## Connection Details

After deployment, you can find connection credentials in the Render dashboard:
- **Host**: Internal service name `mysql`
- **Port**: 3306
- **Database**: `mysql` (also creates `tutordb` for application data)
- **Username**: `mysql`
- **Password**: Auto-generated (check environment variables in Render dashboard)

## Connect from Another Render Service

Add the following environment variables to your application service:
```
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=tutordb
DB_USERNAME=mysql
DB_PASSWORD=$MYSQL_PASSWORD
```

Link your application service to the MySQL service in Render to share the environment variables.

## Local Development

To run this database locally for development:

```bash
docker build -t mysql-tutordb .
docker run -p 3306:3306 -v mysql-data:/var/lib/mysql mysql-tutordb
```
