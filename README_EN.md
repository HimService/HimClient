# HimClient

[Traditional Chinese](README.md) | [English](README_EN.md)

<blockquote style="color: red;">
  <p><strong>Warning!</strong><br>
  We cannot guarantee the advanced security and stability of HimClient. It is recommended to use it for testing and experience purposes only.</p>
</blockquote>


You can go here to view the latest version of the README
https://himservice-docs.himserver.com/#Gemini-Pool/intro

## Introduction

The HimClient project is a server dashboard project based on the Pterodactyl panel, designed to extend the Pterodactyl panel with a user interface for users. This project allows users to log in to the system using their Discord account and create a panel account, enabling them to manage their Pterodactyl server resources through Discord login. The dashboard provides multiple features, including server status monitoring, resource management, a store system, user plan management, and an admin backend, aiming to simplify the management and use of server hosting services.

This project adopts a front-end and back-end architecture. The back-end is responsible for data processing and logic, while the front-end focuses on the user interface experience. Data is stored in an SQLite database, and configuration information is managed through JSON files to ensure system flexibility.

## Project Architecture

This project is mainly composed of the following components:

- **Backend API (Node.js/Express)**:
    - Implemented using `server.js`, based on the Express framework to build a RESTful API service.
    - Responsible for handling all requests from the front-end, including user authentication, database operations, and interaction with the Pterodactyl API.
    - API endpoints cover: You can view the HimClient API documentation [here](https://himservice-docs.himserver.com/#HimClient/api)
    - Database operations use SQLite, interacting via `sqlite3`.
    - Uses `node-fetch` for data exchange with the Pterodactyl API.
    - Task scheduling uses `node-cron`, for example, to periodically check and delete expired servers.

- **Frontend Dashboard (HTML/CSS/JavaScript)**:
    - Located in the `public` directory, developed using HTML, CSS, and JavaScript.
    - Uses `index.html` as the entry point, implementing routing and page rendering through JavaScript.
    - Stores user login status and basic information.
    - The page structure is modular, including a sidebar (`sidebar.js`), home page (`home.js`), login page (`login.js`), dashboard (`dashboard.js`), server management page (`servers.js`), settings page (`settings.js`), store page (`shop.js`), plans page (`plans.js`), AFK earning page (`earn.js`), gift card page (`giftcards.js`), support ticket page (`support.js`), terms page (`terms.js`), admin page (`admin.js`), 404 page (`notfound.js`), and callback page (`callback.js`).
    - Uses CSS (`public/css`) files to define page styles, enhancing the user interface's aesthetics and operational experience.

- **Configuration File (config.json)**:
    - Stores various system configuration information, including:
        - Basic server settings (host address, port).
        - Pterodactyl panel API key and URL.
        - Discord application credentials (client ID, client secret, redirect URI).
        - User plan configuration.
        - Renewal system settings.
        - Store item configuration.
        - Page text content and other static resource settings.
    - Loaded at project startup and used in both the back-end and front-end.

- **Database (database.db)**:
    - Uses an SQLite database file to store user data, server information, and gift card data.
    - The table structure includes `users` (user table), `servers` (server table), and `giftcards` (gift card table).

- **Other Files**:
    - `README.md`: Project documentation.
    - `API.md`: API documentation, detailing all back-end API endpoints.
    - `egg.json`, `server.json`, `shop.json`, `terms.json`: Stores JSON data for server cores, server locations, store items, and terms of use.

## Installation

The following steps will guide you through the installation and setup of the HimClient project:

### Prerequisites

Before starting the installation, please ensure that your system has the following software installed:

1. **Node.js**: It is recommended to use Node.js 16.0 or higher. You can download and install it from the [Node.js official website](https://nodejs.org/).
2. **npm (Node Package Manager)**: npm is usually installed with Node.js. Please ensure that your npm version is 7.0 or higher.

### Installation Steps

1. **Download the Project**:

   You can obtain the project by directly downloading the ZIP archive.

   **Download ZIP Archive**:

   You can download the ZIP archive from the project repository page and extract it to your directory.

2. **Install Node.js Dependencies**:

   In the project root directory, run the following command to install the required Node.js modules:

   ```bash
   npm install
   ```

   This command will automatically install the dependencies as defined in the `package.json` file.

3. **Configure the `config.json` File**:

   You can view example configuration files for `config.json`, `server.json`, etc. [here](https://himservice-docs.himserver.com/#HimClient/set-config)

   **Important**:

   - Be sure to replace `secret` with your own strong password for API request authentication.
   - Create a Discord application in the [Discord Developer Portal](https://discord.com/developers/applications) to obtain the `client_id` and `client_secret`, and set the correct `redirect_uri`.
   - Fill in your Pterodactyl panel URL and API keys. The Application API key needs to be generated in the Pterodactyl admin interface, and the Client API key can be generated in the user settings.

4. **Initialize the Database**:

   When the project is started for the first time, it will automatically create the SQLite database file `database.db` and the necessary table structures. You do not need to create the database manually.

5. **Start the Server**:

   In the project root directory, run the following command to start the server:

   ```bash
   npm start
   ```

   or

   ```bash
   node server.js
   ```

   After the server starts successfully, you will see a system online message in the terminal, displaying the server's running address and port.

6. **Access the Dashboard**:

   Open your browser and visit the URL where the server is running (default is `http://localhost:8080`) to start using the HimClient dashboard.

After completing the above steps, you have successfully installed and configured the HimClient project. If you have any questions, please refer to the project documentation or seek technical support.

## Known Issues

## Development and Contribution

### Reporting Issues

If you find a bug or have a feature suggestion, please create an Issue on GitHub, providing a detailed description and steps to reproduce.

## License

Please read the `LICENSE` file.
