# StuBlogs

StuBlogs is a student-focused blogging website for publishing and discovering articles about health, science, technology, and food. It is built with Express, EJS, and MongoDB, with a responsive server-rendered interface and an admin area for managing posts.

## Features

- Browse published posts, filter by category, and load additional articles.
- View trending stories, top stories, and related posts.
- Register, sign in, and like posts while signed in.
- Create, edit, publish, and delete posts through admin-only pages.
- Write article content in Markdown; rendered HTML is sanitized before display.
- Helmet security headers, login and registration rate limits, and input validation.
- Deploy as a serverless application on Vercel.

## Tech stack

- Node.js and Express 5
- MongoDB with Mongoose
- EJS templates
- JWT authentication stored in an HTTP-only cookie
- `marked` and `sanitize-html` for article rendering

## Run locally

### Requirements

- Node.js and npm
- A MongoDB database (local or hosted)

### Setup

1. Clone the repository and enter the project directory:

   ```bash
   git clone https://github.com/vartika-here/StuBlogs.git
   cd StuBlogs
   ```

2. Install dependencies:

   ```bash
   npm install
   ```

3. Create a `.env` file in the project root:

   ```env
   MONGO_URI=mongodb://127.0.0.1:27017/stublogs
   JWT_SECRET=replace-this-with-a-long-random-secret
   NODE_ENV=development
   PORT=3000
   ```

   `MONGO_URI` can be replaced with `MONGODB_URI`. Use the connection string for your own MongoDB database. Keep `.env` private and never commit real credentials or secrets.

4. Start the development server:

   ```bash
   npm run dev
   ```

   Open [http://localhost:3000](http://localhost:3000). To run without Nodemon, use `npm start`.

## Accounts and admin access

Visitors can register at `/register`. New registrations are assigned the `user` role. Admin pages require an account whose role is `admin`; public registration does not grant admin access. Assign admin access only through a trusted, authorized database administration process.

## Main routes

| Route | Description |
| --- | --- |
| `/` | Homepage, category filters, and paginated posts |
| `/post/:slug` | Published article |
| `/register` | Create an account |
| `/login` | Sign in |
| `/about` | About StuBlogs |
| `/privacy` | Privacy information |
| `/admin/posts` | Admin post management |
| `/admin/create` | Create a post |

Admin routes require an authenticated admin account. Liking a post requires a signed-in user.

## Deploy to Vercel

The repository includes a `vercel.json` configuration for deploying `api/index.js` as a Vercel Node.js function. Import the repository into Vercel and add these environment variables in the project settings:

- `MONGO_URI` (or `MONGODB_URI`): connection string for your MongoDB database.
- `JWT_SECRET`: a long, unique secret used to sign authentication tokens.
- `NODE_ENV`: set to `production`.

Do not commit environment variables to the repository. Ensure the MongoDB deployment allows connections from your hosting environment.

## Project structure

```text
api/             Express application and routes
controllers/     Authentication, post, and admin handlers
middleware/      Authentication and role checks
models/          Mongoose user and post models
public/          Browser-side JavaScript and static assets
scripts/         Database maintenance scripts
views/           EJS pages and shared partials
```

## Scripts

| Command | Description |
| --- | --- |
| `npm run dev` | Start the local server with Nodemon |
| `npm start` | Start the local server with Node.js |
