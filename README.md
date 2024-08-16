# Cooking Recipes Web App - Frontend

This repository contains the frontend application for the Cooking Recipes Web App, a platform that allows users to search, browse, and manage a variety of cooking recipes. The frontend is built using Vue.js, and it interacts with the backend API to retrieve and manipulate data.

## Table of Contents

- [About the Project](#about-the-project)
- [Features](#features)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Scripts](#scripts)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## About the Project

The Cooking Recipes Web App frontend is designed to provide an intuitive and responsive user interface for recipe enthusiasts. Users can create accounts, log in, search for recipes, view detailed recipe instructions, and manage their own recipe collections.

## Features

- **User Authentication**: Secure login and registration for users.
- **Recipe Management**: Create, update, and delete personal recipes.
- **Search and Browse**: Browse through a wide collection of recipes, filter by categories, and search for specific recipes.
- **Responsive Design**: Mobile-friendly design to ensure a seamless experience across devices.
- **State Management**: Vuex is used for managing the application state efficiently.
- **Routing**: Vue Router handles navigation between different pages of the application.

## Project Structure

The project is organized as follows:

```
cooking-recipes-web-app-frontend/
├── public/                # Public assets (e.g., favicon, index.html)
├── src/
│   ├── assets/            # Static assets such as images, icons, etc.
│   ├── components/        # Reusable Vue components
│   ├── router/            # Vue Router setup
│   ├── store/             # Vuex store setup for state management
│   ├── views/             # Components mapped to routes (e.g., Home, Login, RecipeDetail)
│   ├── App.vue            # Root component
│   ├── main.js            # Entry point of the application
├── .env.development       # Environment variables for development
├── .env.production        # Environment variables for production
├── package.json           # Project metadata and dependencies
├── vue.config.js          # Vue CLI configuration
└── README.md              # This file
```

## Installation

To get started with the frontend, follow these steps:

1. **Clone the repository**:
    ```bash
    git clone https://github.com/your_username/cooking-recipes-web-app-frontend.git
    ```

2. **Navigate to the project directory**:
    ```bash
    cd cooking-recipes-web-app-frontend
    ```

3. **Install the dependencies**:
    ```bash
    npm install
    ```

## Configuration

The project includes environment configuration files for different environments:

- **Development**: `.env.development`
- **Production**: `.env.production`

In these files, you can specify environment-specific variables such as the API base URL:

```bash
VUE_APP_API_BASE_URL=http://localhost:5000
```

Update these variables according to your setup.

## Usage

To run the application in development mode, use the following command:

```bash
npm run serve
```

This will start a local development server, and you can view the app by navigating to `http://localhost:8080` in your web browser.

## Scripts

- **`npm run serve`**: Compiles and hot-reloads the app for development.
- **`npm run build`**: Compiles and minifies the app for production.
- **`npm run lint`**: Lints and fixes files.
- **`npm run test:unit`**: Runs unit tests.

## Contributing

Contributions are welcome! If you'd like to contribute to the project, please fork the repository and submit a pull request. Follow the guidelines below:

1. Fork the repository.
2. Create a new branch (`git checkout -b feature/AmazingFeature`).
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`).
4. Push to the branch (`git push origin feature/AmazingFeature`).
5. Open a pull request.

## License

Distributed under the MIT License. See `LICENSE` for more information.

## Contact

Juan J. Rubiales - [jrubialesv@gmail.com](mailto:jrubialesv@gmail.com)

Project Link: [https://github.com/jrubialesv/cooking-recipes-web-app-frontend](https://github.com/jrubialesv/cooking-recipes-web-app-frontend)
