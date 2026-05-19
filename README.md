# CS 371 Capstone Project

A full-stack CRUD web application for interacting with an **Iris dataset** stored in a **PostgreSQL** database. The project includes an **Express.js** backend API and a **React** frontend interface that allows users to create, read, update, and delete dataset records through a simple browser-based UI.

## Overview

This project demonstrates how to build a complete client-server application with a database-backed API. It provides a practical interface for managing Iris flower records and viewing aggregated statistics by species.

Users can:
- View summary statistics for Iris species
- Add new dataset records
- Update existing records
- Delete records by serial number
- Upload JSON files to prefill form data for create and update operations

The backend exposes RESTful endpoints that communicate with a PostgreSQL database, while the frontend presents an interactive React-based interface for performing CRUD actions.

## Features

- **Full CRUD functionality**
  - Create new Iris records
  - Read grouped dataset statistics
  - Update existing records by serial number
  - Delete records by serial number

- **Statistics dashboard**
  - Aggregated species-level statistics
  - Average, minimum, and maximum measurements for sepal and petal features
  - Species count breakdown

- **Interactive React frontend**
  - Separate UI components for GET, POST, PUT, and DELETE operations
  - Dynamic success and error messaging
  - Table-based result rendering

- **JSON upload support**
  - Upload JSON files to populate form fields for record creation and editing

- **Database-backed API**
  - PostgreSQL integration using `pg`
  - Express.js REST endpoints for data operations

## Tech Stack

- **Frontend:** React, JavaScript, CSS
- **Backend:** Node.js, Express.js
- **Database:** PostgreSQL
- **Configuration:** dotenv

## Project Structure

```text name=project-structure.txt
cs-371_capstone_project/
├── backend/
│   ├── package.json       # Backend dependencies and scripts
│   └── server.js          # Express server and API routes
└── frontend/
    └── src/
        ├── App.js         # Main application component
        ├── App.css        # App-specific styling
        ├── index.css      # Global styling
        └── Components/
            ├── DeleteComponent.js   # Delete record UI
            ├── GetComponent.js      # Fetch statistics UI
            ├── PostComponent.js     # Add record UI
            ├── PutComponent.js      # Update record UI
            └── ResponseTable.js     # Result display table
```

## Architecture

### Frontend
The React frontend provides a button-driven interface for selecting CRUD operations. Each operation is implemented as its own component, making the UI modular and easier to maintain.

- `App.js` manages the active view, API calls, success messages, and error handling
- `GetComponent.js` fetches and displays aggregated dataset statistics
- `PostComponent.js` handles inserting new records
- `PutComponent.js` updates existing records
- `DeleteComponent.js` removes records by serial number
- `ResponseTable.js` renders returned API data in a readable table format

### Backend
The Express backend connects to a PostgreSQL database using a connection pool.

`server.js` defines endpoints for:
- retrieving species-level summary statistics
- inserting new Iris records
- updating records by serial number
- deleting records by serial number

The database connection is configured through environment variables loaded with `dotenv`.

## API Endpoints

### `GET /iris`
Returns grouped summary statistics for the Iris dataset by species, including:
- record count
- average sepal length and width
- average petal length and width
- minimum and maximum sepal length
- minimum and maximum petal length

### `POST /iris`
Adds a new record to the Iris table.

Expected JSON body:

```json name=post-body.json
{
  "serial_number": "101",
  "sepal_length": 5.1,
  "sepal_width": 3.5,
  "petal_length": 1.4,
  "petal_width": 0.2,
  "species": "Iris-setosa"
}
```

### `PUT /iris/:serial_number`
Updates an existing Iris record identified by `serial_number`.

### `DELETE /iris/:serial_number`
Deletes an existing Iris record identified by `serial_number`.

## Setup Instructions

## 1. Clone the repository

```bash name=clone.sh
git clone https://github.com/cchinmay7/cs-371_capstone_project.git
cd cs-371_capstone_project
```

## 2. Backend setup

Navigate to the backend folder and install dependencies:

```bash name=backend-setup.sh
cd backend
npm install
```

Create a `.env` file in the `backend` directory:

```env name=backend/.env.example
PORT=8000
DB_USER=your_database_user
DB_HOST=your_database_host
DB_NAME=your_database_name
DB_PASSWORD=your_database_password
DB_PORT=5432
```

Start the backend server:

```bash name=backend-run.sh
npm start
```

## 3. Frontend setup

In a separate terminal, navigate to the frontend project and install dependencies if needed.

If this frontend was created with Create React App or a similar React setup, run:

```bash name=frontend-setup.sh
cd frontend
npm install
npm start
```

> Note: This repository snapshot includes `frontend/src`, but the exact frontend package configuration is not visible in the files reviewed. If a `package.json` exists in the frontend directory locally, use it to install and run the React app.

## Database Requirements

This project expects a PostgreSQL database containing an `iris` table with fields similar to:
- `serial_number`
- `sepal_length`
- `sepal_width`
- `petal_length`
- `petal_width`
- `species`

A sample schema could look like:

```sql name=iris-schema.sql
CREATE TABLE iris (
  serial_number VARCHAR(50) PRIMARY KEY,
  sepal_length NUMERIC,
  sepal_width NUMERIC,
  petal_length NUMERIC,
  petal_width NUMERIC,
  species VARCHAR(100)
);
```

## Example Workflow

1. Start the backend server.
2. Start the frontend development server.
3. Open the React app in the browser.
4. Use the navigation buttons to select GET, POST, PUT, or DELETE.
5. Submit forms to interact with the PostgreSQL-backed Iris dataset.
6. View returned results and success messages in the UI.

## Strengths of the Project

- Clear separation between frontend and backend
- Practical demonstration of REST API design
- Useful example of PostgreSQL integration in Node.js
- Strong educational example of full-stack CRUD application development
- Includes grouped analytical queries in addition to basic CRUD operations

## Current Limitations / Improvement Opportunities

- The frontend API base URL is hardcoded and should be moved to environment configuration
- No authentication or authorization layer is implemented
- Validation and error messages could be more detailed
- The frontend setup files were not fully visible in the repository structure reviewed
- No automated test suite is currently included
- CORS handling may need to be added depending on frontend/backend deployment setup

## Future Enhancements

- Add filtering and search for dataset records
- Add charts or visualizations for species statistics
- Support bulk upload of Iris records
- Add input validation and form feedback
- Move configuration values into environment files for both frontend and backend
- Add automated testing for API endpoints and UI components
- Deploy the frontend and backend with cloud hosting

## License

This repository currently does not specify a project license.

## Author

Created by **cchinmay7** for a CS 371 capstone project.
