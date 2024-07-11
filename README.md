# Basic Gulp Setup for Web Development

This project includes a basic setup for using Gulp to automate tasks in web development. Gulp is a powerful tool that helps with tasks like starting a development server, compiling Sass to CSS, adding vendor prefixes, minifying CSS, and live-reloading the browser when files change.

## Node.js and Gulp

Make sure you have the following installed on your system:

- [Node.js](https://nodejs.org/) (includes npm)
- [Gulp](https://gulpjs.com/)

## Getting Started

## Short Description of Each Command

1. **Initialize npm project**:

   ```sh
   npm init
   ```

   Initializes a new Node.js project and creates a `package.json` file.

2. **Install Gulp CLI globally**:

   ```sh
   npm install gulp-cli --save-dev
   ```

   Installs the Gulp command-line interface globally for running Gulp tasks.

3. **Install Gulp locally**:

   ```sh
   npm install gulp --save-dev
   ```

   Installs Gulp locally in your project for task automation.

4. **Install Gulp Sass plugin**:

   ```sh
   npm install gulp-sass --save-dev
   ```

   Installs the Gulp plugin for compiling Sass to CSS.

5. **Install BrowserSync globally**:

   ```sh
   npm install -g browser-sync
   ```

   Installs BrowserSync globally to sync file changes and reload the browser.

6. **Install BrowserSync locally**:

   ```sh
   npm install browser-sync --save-dev
   ```

   Installs BrowserSync locally in your project.

7. **Install Gulp Autoprefixer**:

   ```sh
   npm install gulp-autoprefixer@8.0.0 --save-dev
   ```

   Installs the Gulp plugin for adding vendor prefixes to CSS.

8. **Install Gulp Clean CSS plugin**:

   ```sh
   npm install gulp-clean-css --save-dev
   ```

   Installs the Gulp plugin for minifying CSS files.

9. **Install Sass compiler**:

   ```sh
   npm install sass --save-dev
   ```

   Installs the Sass compiler to compile Sass files.

10. **Install Gulp Rename plugin**:

```sh
npm install gulp-rename --save-dev
```

## Gulpfile.js

Create `gulpfile.js` with the following code, its used for the tasks:

```javascript
// Import necessary packages
const gulp = require("gulp");
const browserSync = require("browser-sync");
const sass = require("gulp-sass")(require("sass"));
const cleanCSS = require("gulp-clean-css");
const autoprefixer = require("gulp-autoprefixer");
const rename = require("gulp-rename");

// Task to set up a server with BrowserSync
gulp.task("server", function () {
  browserSync({
    server: {
      baseDir: "src", // Serve files from the "src" directory
    },
  });

  // Watch HTML files in the "src" directory for changes and reload the browser
  gulp.watch("src/*.html").on("change", browserSync.reload);
});

// Task to compile Sass files, add prefixes, minify CSS, and stream changes to BrowserSync
gulp.task("styles", function () {
  return gulp
    .src("src/sass/**/*.+(scss|sass)")
    .pipe(sass({ outputStyle: "compressed" }).on("error", sass.logError))
    .pipe(rename({ suffix: ".min", prefix: "" }))
    .pipe(autoprefixer())
    .pipe(cleanCSS({ compatibility: "ie8" }))
    .pipe(gulp.dest("src/css"))
    .pipe(browserSync.stream());
});

// Task to watch Sass files for changes and re-run the 'styles' task
gulp.task("watch", function () {
  gulp.watch("src/sass/**/*.+(scss|sass)", gulp.parallel("styles"));
});

// Default task that runs when you type "gulp" in the command line
gulp.task("default", gulp.parallel("watch", "server", "styles"));
```

````

### Run Server

Run the server with the following command in your terminal:

```sh
gulp
```

Ensure your project has the following structure:

````

    yourproject/
    ├── src/
    │   ├── css/
    │   ├── sass/
    │   │   └── style.scss
    │   ├── images/
    │   └── index.html
    ├── gulpfile.js
    └── package.json
    ```````
