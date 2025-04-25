# PostgreSQL CSV Export

A simple Node.js application for seeding a PostgreSQL database with sample product data and exporting it to CSV format.

## Features

- Database connection using the `postgres` library
- Seeding the database with fake product data using Faker.js
- Exporting database query results to CSV files using streams for memory efficiency

## Prerequisites

- Node.js v23+
- PostgreSQL database
- pnpm (or npm/yarn)

## Setup

1. Clone the repository
2. Install dependencies:
   ```
   pnpm install
   ```
3. Create a `.env.local` file with your database connection string:
   ```
   DATABASE_URL=postgres://username:password@localhost:5432/database
   ```

## Using Docker Compose

This project includes a Docker Compose configuration for easily setting up a PostgreSQL database.

1. Start the PostgreSQL container:
   ```bash
   docker-compose up -d
   ```

2. Configure your `.env.local` file to connect to the Docker container:
   ```
   DATABASE_URL=postgres://postgres:postgres@localhost:5432/postgres
   ```

3. Stop the database when you're done:
   ```bash
   docker-compose down
   ```

   To remove the database volume as well:
   ```bash
   docker-compose down -v
   ```

## Usage

### Seeding the Database

Run the seed script to create the products table and populate it with sample data:

```bash
node --env-file .env.local src/db/seed.ts
```

This will:
- Create a `products` table if it doesn't exist
- Clear any existing data in the table
- Insert 100,000 sample products (10 batches of 10,000 products)

### Exporting to CSV

Run the export script to generate a CSV file from the database:

```bash
node --env-file .env.local src/export.ts
```

This will:
- Query products with a price greater than 1000 cents
- Stream the results to a CSV file named `export.csv`
- Use memory-efficient Node.js streams to handle large datasets

## Project Structure

- `src/db/client.ts` - Database connection setup
- `src/db/seed.ts` - Script to seed the database with sample data
- `src/export.ts` - Script to export database query results to CSV
- `.env.local` - Environment variables (not committed to git)

## Technologies

- TypeScript
- Node.js
- PostgreSQL
- Faker.js for generating sample data
- csv-stringify for CSV generation
- Node.js streams for memory-efficient processing
