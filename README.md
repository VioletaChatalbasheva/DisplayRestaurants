# Display Restaurants

A web application for viewing and managing restaurant information.

## Features

- Display list of the first 10 restaurants
- View restaurant details

## Technologies

- Vue.js
- HTML/CSS
- JavaScript

#### Requirements

| Name | Link |
|---|---|
| NodeJS and Npm | [NodeJS and Npm installation](https://www.npmjs.com/get-npm) |
| VisualStudio Code (recommended) | [VS Code download](https://code.visualstudio.com/download) |

## Installation

#### Clone

Clone this repo to your local machine using

```
https://github.com/VioletaChatalbasheva/DisplayRestaurants.git
```

#### Install Requirements

Move to  the application folder and run in your terminal:
```
npm install
```

#### Install Requirements

Move to  the application folder and run in your terminal:
```
npm run dev -- --port 3000
```

Navigate to `http://localhost:3000/` in your browser. The app will automatically reload if you change any of the source files.

## Assumptions

1. I assumed the provided API endpoint returns a list of restaurants with the necessary fields (name, cuisines, rating, address).
2. Since the API only works for UK postcodes, I defined a list with the postcodes given in the assignment which the user can choose from.
3. I assume that restaurants with rating above 3 are more likely to be preffered by the users so the UI shows a golden star. If the rating is lower, the user sees only the rating number.
4. The full list of cuisines is displayed which assumes the data returned by the backend is correct. However, I noticed that the cuisines data also contains information about the special offers in the restaurant, so the data displayed in the user interface is not only limited to cuisines.

## Improvements

1. The API was returning an empty array for the restaurants due to a CORS issue. To access the API data, I used ThingProxy (a public CORS proxy). A better and more robust solution would be implmenting a server-side proxy.
2. The user interface could be enhanced by:
   - Including a map view for restaurant locations
   - Making the design more engaging for the user
