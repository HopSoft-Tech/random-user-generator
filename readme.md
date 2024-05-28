# Random User Generator

## Overview

The Random User Generator is a web application that fetches and displays random user data from an external API. The application allows users to generate random user profiles including information such as name, email, phone number, location, and age. Additionally, the background color of the page changes based on the gender of the generated user.

## Features

- **Random User Profiles**: Generate random user profiles with detailed information.
- **Dynamic Background Color**: Changes the background color based on the user's gender.
  - Lavender for female users.
  - Slategray for male users.
- **Responsive Design**: A user-friendly interface designed with Tailwind CSS for responsiveness and modern look.
- **Spinner Animation**: Displays a loading spinner while fetching data from the API.

## Technologies Used

- **HTML**: For the structure of the web application.
- **CSS**: For basic styling and layout.
- **Tailwind CSS**: For advanced and responsive styling.
- **JavaScript**: For fetching data from the API and dynamically updating the DOM.
- **Random User API**: An external API used to fetch random user data.

## How It Works

1. **Initial Setup**: The web page loads with a button labeled "Generate User."
2. **Fetching Data**: When the button is clicked, a request is sent to the Random User API.
3. **Displaying Data**: The application parses the response and displays the user’s profile information on the screen.
4. **Background Color**: The background color changes based on the gender of the user.
   - Female: pink
   - Male: steelblue

## Installation

To run this application locally, follow these steps:

1. **Clone the repository**:

   ```bash
   git clone https://github.com/HopSoft-Tech/random-user-generator.git
   ```

2. **Navigate to the project directory**:

   ```bash
   cd random-user-generator
   ```

3. **Open `index.html` in your browser**:
   ```bash
   open index.html
   ```

## Usage

1. Open the application in your web browser.
2. Click on the "Generate User" button.
3. Wait for the spinner to disappear and the user profile to be displayed.
4. Observe the dynamic background color change based on the user's gender.

## Code Explanation

### HTML

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="spinner.css" />
    <script src="https://cdn.tailwindcss.com"></script>
    <title>Random User Generator</title>
  </head>
  <body class="bg-white text-white overflow-x-hidden">
    <div
      class="relative max-w-2xl m-auto mt-12 border border-white rounded-lg p-4"
    >
      <div class="text-center">
        <h1 class="text-2xl">Random User Generator</h1>
        <button
          id="generate"
          class="relative bg-black text-white px-4 py-2 rounded w-full my-4"
        >
          <div class="spinner hidden"></div>
          Generate User
        </button>
      </div>
      <div id="user" class="mt-6"></div>
    </div>
    <script src="./script.js"></script>
  </body>
</html>
```

### JavaScript

```javascript
function fetchUser() {
  showSpinner();
  fetch("https://randomuser.me/api")
    .then((res) => res.json())
    .then((data) => {
      hideSpinner();
      displayUser(data.results[0]);
    });
}

function displayUser(user) {
  const userDisplay = document.querySelector("#user");

  if (user.gender === "female") {
    document.body.style.backgroundColor = "pink";
  } else {
    document.body.style.backgroundColor = "steelblue";
  }

  userDisplay.innerHTML = `
  <div class="flex justify-between">
    <div class="flex">
      <img class="w-48 h-48 rounded-full mr-8" src="${user.picture.large}" />
      <div class="space-y-3">
        <p class="text-xl"><span class="font-bold">Name: </span>${user.name.first} ${user.name.last}</p>
        <p class="text-xl"><span class="font-bold">Email: </span>${user.email}</p>
        <p class="text-xl"><span class="font-bold">Phone: </span>${user.phone}</p>
        <p class="text-xl"><span class="font-bold">Location: </span>${user.location.city} ${user.location.country}</p>
        <p class="text-xl"><span class="font-bold">Age: </span> ${user.dob.age}</p>
      </div>
    </div>
  </div>`;
}

function showSpinner() {
  document.querySelector(".spinner").style.display = "block";
}

function hideSpinner() {
  document.querySelector(".spinner").style.display = "none";
}

document.querySelector("#generate").addEventListener("click", fetchUser);

fetchUser();
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [Random User API](https://randomuser.me/) for providing the user data.
- [Tailwind CSS](https://tailwindcss.com/) for styling the application.
