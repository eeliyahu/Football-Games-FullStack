# Football Games Project

A full-stack web application for displaying football game results, upcoming fixtures, and providing access to YouTube highlight videos. The project consists of a Node.js/Express backend with Firebase Functions and an Angular frontend.

## 🚀 Features

- **Football Game Information**: View recent and historical football game results, as well as future fixtures
- **YouTube Highlights**: Access YouTube highlight videos for individual matches
- **Search Functionality**: Search for games by date, team, and other criteria
- **Firebase Integration**: Utilizes Firebase for data storage and hosting
- **Multi-League Support**: Covers major European leagues (Spain, England, France, Germany, Italy)

## 📁 Project Structure

The project consists of two main components:
- **customer-app**: Angular frontend application
- **Server**: Node.js/Express backend with Firebase Functions support

## 🛠️ Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (LTS version recommended)
- **npm** (comes with Node.js)
- **Angular CLI**: `npm install -g @angular/cli`
- **Firebase CLI**: `npm install -g firebase-tools`

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone <repository_url>
cd <repository_name>
```

### 2. Server Setup

Navigate to the Server directory:

```bash
cd Server
```

Install dependencies:

```bash
npm install
```

#### Local Development (Server)

To run the server locally on port 3000:

```bash
node server.js
```

#### Firebase Functions Deployment (Server)

To deploy the server as a Firebase Function:

```bash
cd functions
npm install
cd .. # Go back to the Server directory
firebase deploy --only functions
```

### 3. Customer App Setup

Navigate to the customer-app directory:

```bash
cd ../customer-app
```

Install dependencies:

```bash
npm install
```

#### Local Development (Customer App)

To run the Angular application locally:

```bash
ng serve
```

The application will be available at `http://localhost:4200/`

#### Firebase Hosting Deployment (Customer App)

To build and deploy the Angular application:

```bash
ng build --prod
firebase deploy --only hosting
```

## 🔌 API Endpoints

The server exposes the following REST API endpoints:

### Base Endpoint
- **GET** `/`
  - **Description**: Health check endpoint
  - **Response**: `<h1>Football Games Server</h1> Server is running successfully</p>`

### Game Data
- **GET** `/getGames/`
  - **Description**: Retrieves football game data
  - **Query Parameters**:
    - `team` (optional): Team ID to filter games (default: '83')
    - `year` (optional): Season year or 'Upcoming' for future fixtures (default: current year)
  - **Example**: `/getGames/?team=83&year=2024` or `/getGames/?year=Upcoming`

### Video Highlights
- **GET** `/getVideo/`
  - **Description**: Retrieves YouTube video ID for match highlights
  - **Query Parameters**:
    - `teamString`: Team names (e.g., "Barcelona vs Real Madrid")
    - `score`: Match score (e.g., "3-2")
    - `year`: Match year
  - **Response**: `{ videoId: '...' }` or `{ videoId: '' }` if no video found

### Team Management
- **GET** `/saveTeamsInFirebase/`
  - **Description**: Populates Firebase with team information for major European leagues
  - **Response**: "Teams added successfully!" or error message

- **GET** `/getTeams/`
  - **Description**: Retrieves saved team and country information
  - **Response**: JSON object with country data including teams, league, and code properties

### Utility
- **GET** `/countriesFlags/`
  - **Description**: Retrieves country codes and names for flag display
  - **Response**: JSON object mapping country codes to names

## ⚙️ Firebase Configuration

The Firebase configuration is embedded in both `server.js` and `functions/index.js`:

```javascript
var firebaseConfig = {
    apiKey: "AIzaSyDvCJuvLuJl4UKgDuNeFQYPuKypcJN5GlI",
    authDomain: "football-games-project.firebaseapp.com",
    databaseURL: "https://football-games-project-default-rtdb.firebaseio.com",
    projectId: "football-games-project",
    storageBucket: "football-games-project.appspot.com",
    messagingSenderId: "1050505135501",
    appId: "1:1050505135501:web:6b902ff5e73cd6e3c9a9c4",
    measurementId: "G-F5LDPBQ1D6"
};
```

## 🔐 Security Considerations

⚠️ **Important**: The YouTube Data API key is currently embedded directly in the server files. For production environments, it is highly recommended to:

- Use environment variables to store API keys
- Implement a dedicated secrets management service
- Restrict API key usage by domain/IP address

## 📦 Dependencies

For a complete list of dependencies, refer to the `package.json` files in both:
- `Server/package.json` - Backend dependencies
- `customer-app/package.json` - Frontend dependencies

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. Contribution guidelines will be added in future updates.

## 📄 License

License information will be added in future updates.

## 🏗️ Architecture

- **Frontend**: Angular application with Firebase hosting
- **Backend**: Node.js/Express server deployable as Firebase Functions
- **Database**: Firebase Realtime Database
- **External APIs**: 
  - Football data API for game information
  - YouTube Data API for highlight videos

## 🔧 Development Notes

- The server can run both locally (`server.js`) and as a Firebase Function (`functions/index.js`)
- The Angular app is configured for both local development and Firebase hosting deployment
- Team data supports major European leagues with automatic population via API endpoints
