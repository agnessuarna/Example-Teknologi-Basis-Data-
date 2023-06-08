# Example-Source-Code-Frontend (UI)

Source ini menggunakan React js dan Tailwinds CSS.

Source Code ini untuk Frontend (Bagian UI)nya

## How to Run this Source Code in Local 
- Clone this project on your computer.
  ```bash
     https://github.com/agnessuarna/Example-Teknologi-Basis-Data-.git
   ```
### Frontend

Go to the frontend project directory

```bash
  cd frontend
```

Install dependencies

```bash
  npm install
```

Run the app in development mode

```bash
  npm run start
```

## Backend: Presenting Data from PostgreSQL
To present data from a PostgreSQL database using Node.js in an HTML format, you can use a template engine like EJS (Embedded JavaScript).

While this repository only contains frontend codebase, here's an example code that demonstrates how to fetch data from PostgreSQL and render it in a simple HTML template using Node.js and EJS:

1. First, install the required packages by running the following command in your project directory:
  ```bash
  npm install express pg ejs
  ```
2. Create an HTML template file called `index.ejs` in your project directory with the following content:
```html
<!DOCTYPE html>
<html>
<head>
  <title>Data Presentation</title>
</head>
<body>
  <h1>Data Presentation</h1>
  <table>
    <thead>
      <tr>
        <th>ID</th>
        <th>Name</th>
        <th>Email</th>
      </tr>
    </thead>
    <tbody>
      <% data.forEach(function(row) { %>
        <tr>
          <td><%= row.id %></td>
          <td><%= row.name %></td>
          <td><%= row.email %></td>
        </tr>
      <% }); %>
    </tbody>
  </table>
</body>
</html>
```

3. Create a file called `app.js` (or any other preferred name) with the following code:
```javascript
const express = require('express');
const { Client } = require('pg');
const app = express();
const port = 3000;

// Configure the PostgreSQL connection
const config = {
  user: 'your_username',
  password: 'your_password',
  host: 'localhost',
  port: 5432,
  database: 'your_database_name'
};

// Create a new PostgreSQL client instance
const client = new Client(config);

// Connect to the database
client.connect();

// Define a route to fetch data from the database
app.get('/', (req, res) => {
  // Query the database and fetch data
  client.query('SELECT * FROM your_table_name')
    .then((result) => {
      // Render the HTML template with the fetched data
      res.render('index', { data: result.rows });
    })
    .catch((err) => {
      console.error('Error:', err);
      res.send('An error occurred');
    });
});

// Start the server
app.listen(port, () => {
  console.log(`Server listening on port ${port}`);
});
```
Replace `'your_username'`, `'your_password'`, `'localhost'`, `'your_database_name'`, and `'your_table_name'` in `app.js` with your PostgreSQL configuration and table name.

4. Run the application by executing the following command:
```bash
node app.js
```
Open your web browser and visit http://localhost:3000. You should see the data from your PostgreSQL table rendered in an HTML table format.

Make sure you have a PostgreSQL server running and accessible with the provided configuration. Adjust the table structure and HTML template as per your specific data requirements and presentation style.
