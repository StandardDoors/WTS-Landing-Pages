# WTS Landing Pages

Static landing pages for WTS (Windows That Seal), built with PHP and deployed to GitHub Pages.

## Overview

This project uses PHP as a static site generator. PHP files in the `src/` directory are processed into static HTML files during the build process, making the site fast and easy to deploy on any static hosting platform.

## Requirements

- PHP 8.1 or higher
- Composer

## Installation

Install dependencies:

    composer install

## Local Development

### Development Server

Start the built-in PHP development server to preview changes:

    composer serve

This starts a server at `http://localhost:8000` serving files from the `src/` directory.

Press `Ctrl+C` to stop the server.

### Making Changes

1. Edit PHP files in `src/` directory
2. Refresh your browser to see changes
3. Partials are in `src/partials/` (header.php, footer.php)
4. Assets are in `src/assets/`

## Building

Generate static HTML files:

    composer build

This creates a `dist/` directory with:
- All `.php` files converted to `.html`
- Assets copied from `src/assets/`
- Favicon files copied

Build output:

    🔨 Building static site...
    
    🧹 Cleaning dist directory...
    📄 Processing PHP files...
      • wts-en.php → wts-en.html
      • wts-fr.php → wts-fr.html
      • wts-bi.php → wts-bi.html
      • wts-dev.php → wts-dev.html
      • wts-usa.php → wts-usa.html
      • wts-rona-en.php → wts-rona-en.html
      • wts-rona-fr.php → wts-rona-fr.html
    📦 Copying assets...
    🎨 Copying favicon files...
      • favicon.ico
      • favicon.gif
    
    ✅ Build complete! Built 7 pages.
    📁 Output directory: dist/

## Testing

Run the test suite to verify build functionality:

    composer test

Tests verify:
- Build creates dist directory
- All PHP files are converted to HTML
- Generated HTML is valid
- Assets are copied correctly
- PHP code is fully processed (no raw PHP in output)

## Project Structure

    .
    ├── src/                      # Source files
    │   ├── assets/               # Images, CSS, JavaScript
    │   ├── partials/             # Reusable PHP components
    │   │   ├── header.php
    │   │   └── footer.php
    │   ├── wts-en.php            # English landing page
    │   ├── wts-fr.php            # French landing page
    │   ├── wts-bi.php            # Bilingual landing page
    │   ├── wts-dev.php           # Development page
    │   ├── wts-usa.php           # USA landing page
    │   ├── wts-rona-en.php       # Rona English page
    │   └── wts-rona-fr.php       # Rona French page
    ├── dist/                     # Generated static files (ignored in git)
    ├── tests/                    # Test files
    ├── build.php                 # Build script
    ├── composer.json             # Dependencies and scripts
    └── README.md

## Deployment

### GitHub Pages (Automatic)

The site is automatically built and deployed to GitHub Pages when you push to the `main` branch.

GitHub Actions workflow:
1. Checks out code
2. Installs PHP and Composer
3. Runs `composer install`
4. Runs `composer build`
5. Deploys `dist/` to GitHub Pages

View the workflow: `.github/workflows/build-deploy.yml`

### Manual Deployment

Build locally and deploy the `dist/` directory to any static hosting:

    composer build
    
    # Deploy dist/ to your hosting provider

Supported platforms:
- GitHub Pages
- Netlify
- Vercel
- AWS S3
- Any static file hosting

## Available Scripts

- `composer build` - Build static site
- `composer serve` - Start development server
- `composer test` - Run tests
- `composer clean` - Remove dist directory

## How It Works

### Build Process

1. **Clean**: Remove existing `dist/` directory
2. **Process PHP**: Execute each `.php` file in `src/` and capture output as HTML
3. **Copy Assets**: Copy `src/assets/` to `dist/assets/`
4. **Copy Favicons**: Copy favicon files to `dist/`

### PHP to HTML Conversion

PHP files use standard includes and variables:

    <?php
    $pageTitle = 'WTS Home Tab EN';
    include 'partials/header.php';
    ?>
    <div class="centerimage">
        <a href="https://standarddoors.com/" target="_blank">
            <img src="assets/logos/LogoStandardColourEN2024.png">
        </a>
    </div>
    <?php include 'partials/footer.php'; ?>

During build, this becomes static HTML with all PHP processed and includes resolved.

## Troubleshooting

### Build fails

Check PHP version:

    php --version

Ensure PHP 8.1 or higher is installed.

### Changes not appearing

Make sure you're:
1. Editing files in `src/` not `dist/`
2. Running `composer build` after changes
3. Refreshing your browser with cache cleared

### Assets not loading

Verify asset paths use relative paths:
- ✅ `assets/logos/logo.png`
- ❌ `/assets/logos/logo.png`
- ❌ `../assets/logos/logo.png`

## License

Proprietary - Standard Doors
