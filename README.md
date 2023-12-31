# Pokémon API Documentation

[Deployed URL](https://pokemon-backend-dfea.onrender.com/api/pokemon/)

## Overview

This document provides detailed information about the Pokémon API, which allows users to retrieve Pokémon data with various options like pagination, sorting, and sorting order. It is built using Node.js and Express.

## Getting Started

These instructions will guide you through getting a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

What things you need to install the software:

-   [Node.js](https://nodejs.org/)
-   npm (Node.js package manager, comes with Node.js installation)

### Installing

1. **Clone the repository** - Clone the project repository to your local machine using the following command:

    ```bash
    git clone <repository-url>
    ```

    Replace `<repository-url>` with the URL of this repository.

2. **Navigate to the project directory**:

    ```bash
    cd <repository-directory>
    ```

    Replace `<repository-directory>` with the name of the folder where the repository was cloned.

3. **Install dependencies** - Install the necessary project dependencies by running:

    ```bash
    npm install
    ```

    This command will install all the dependencies listed in the `package.json` file.

4. **Start the server** - Once the dependencies are installed, start the server with:

    ```bash
    npm start
    ```

    This will start the local development server. By default, it will run on `http://localhost:8081`.

5. **Verify the server is running** - Open your web browser and navigate to `http://localhost:8081`. If the server is running, you should see a message or output relevant to the Pokémon API.

### Testing

To ensure everything is set up correctly, you can test the API using a tool like [Postman](https://www.postman.com/) or a simple `curl` command in the terminal:

````bash
curl -X GET "http://localhost:8081/api/pokemon"
````

# Pokémon API

The Pokémon API provides access to a list of Pokémon with features like pagination, sorting, and CRUD (Create, Read, Update, Delete) operations. It is built using Node.js and Express.

## API Reference

### Get List of Pokémon

`GET /api/pokemon`

Returns a paginated list of Pokémon with sorting options.

#### Query Parameters

- `limit` (optional): Number of Pokémon to return per page. Default is 200.
- `offset` (optional): Number of Pokémon to skip before starting to return. Default is 0.
- `sort` (optional): Attribute to sort the Pokémon by (e.g., 'name', 'height', 'weight').
- `order` (optional): Order of the sorting. Can be 'asc' for ascending or 'desc' for descending. Default is ascending.
- `type` (optional): Filter Pokémon by type (e.g., 'fire', 'water').

#### Sample Request

```bash
curl -X GET "http://localhost:8081/api/pokemon?limit=50&offset=0&sort=name&order=asc&type=fire"
```

### Get a Single Pokémon

`GET /api/pokemon/:name`

Fetches details of a specific Pokémon by its name.

#### URL Parameters

- `name`: Name of the Pokémon to retrieve.

#### Sample Request

```bash
curl -X GET "http://localhost:8081/api/pokemon/bulbasaur"
```

#### Response Fields

The response contains a JSON object with the following fields for a Pokémon:

- `id`: The unique identifier for the Pokémon.
- `name`: The name of the Pokémon.
- `official_artwork_default`: The URL to the official artwork of the Pokémon.
- `height`: The height of the Pokémon.
- `weight`: The weight of the Pokémon.
- `isDefault`: Boolean indicating if this is the default form.
- `types`: An array of types that the Pokémon belongs to (e.g., `["grass", "poison"]`).
- `alt_images`: An array of alternative images, each object containing:
  - `title`: A descriptive title for the image.
  - `url`: The URL to the image.
- `moves`: An array of move names that the Pokémon can learn.
- `abilities`: An array of ability names that the Pokémon has.
- `base_stats`: An object containing the base stats, with fields like `hp`, `attack`, `defense`, `special-attack`, `special-defense`, `speed`.

#### Sample Request

```bash
curl -X GET "http://localhost:8081/api/pokemon/bulbasaur"
```

#### Sample Response

```json
{
  "id": 1,
  "name": "bulbasaur",
  "official_artwork_default": "https://example.com/artwork/bulbasaur.png",
  "height": 7,
  "weight": 69,
  "isDefault": true,
  "types": ["grass", "poison"],
  "alt_images": [
    {
      "title": "Front Default",
      "url": "https://example.com/images/front_default.png"
    },
    // More images...
  ],
  "moves": ["tackle", "vine whip", "growl"],
  "abilities": ["overgrow", "chlorophyll"],
  "base_stats": {
    "hp": 45,
    "attack": 49,
    "defense": 49,
    "special-attack": 65,
    "special-defense": 65,
    "speed": 45
  }
}
```

### Create a New Pokémon

`POST /api/pokemon`

Creates a new Pokémon entry.

#### Request Body

- JSON object containing Pokémon details.

#### Sample Request

```bash
curl -X POST "http://localhost:8081/api/pokemon" -H "Content-Type: application/json" -d '{ "name": "newpokemon", "height": 10, "weight": 200, ... }'
```

### Update an Existing Pokémon

`PUT /api/pokemon/:name`

Updates details of an existing Pokémon.

#### URL Parameters

- `name`: Name of the Pokémon to update.

#### Request Body

- JSON object containing updated Pokémon details.

#### Sample Request

```bash
curl -X PUT "http://localhost:8081/api/pokemon/bulbasaur" -H "Content-Type: application/json" -d '{ "height": 8, "weight": 250, ... }'
```

### Delete a Pokémon

`DELETE /api/pokemon/:name`

Deletes a Pokémon from the list.

#### URL Parameters

- `name`: Name of the Pokémon to delete.

#### Sample Request

```bash
curl -X DELETE "http://localhost:8081/api/pokemon/bulbasaur"
```
