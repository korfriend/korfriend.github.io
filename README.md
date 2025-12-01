# Lab Homepage

This is the source code for the Lab Homepage, built with [Jekyll](https://jekyllrb.com/).

## Prerequisites

- **Ruby 3.3+** (with DevKit)
- **Bundler** & **Jekyll**
- **Node.js** (for local admin backend)

## Local Development Setup

### 1. Install Dependencies

If you haven't already, install the required Ruby gems:

```powershell
bundle install
```

### 2. Run the Website

To start the local Jekyll server:

```powershell
# Standard command (if Ruby is in your PATH)
bundle exec jekyll serve

# OR, if you encounter PATH issues with Ruby 3.3 on Windows, use this robust command:
cmd /c "set PATH=C:\Ruby33-x64\bin;%PATH% && ruby.exe C:\Ruby33-x64\bin\bundle exec jekyll serve"
```

The site will be available at: **[http://localhost:4000](http://localhost:4000)**

### 3. Run the Admin Interface (Decap CMS)

To edit content (like Team Members) locally using the Admin UI:

1.  **Start the Proxy Server** (in a new terminal):
    ```powershell
    npx decap-server
    ```

2.  **Access the Admin Panel**:
    Go to **[http://localhost:4000/admin/](http://localhost:4000/admin/)**

3.  **Login**:
    Click "Login with Netlify Identity" (or similar). Since it's running locally, it will bypass authentication.

### 4. Editing Content

- **Team Members**: Managed via the Admin panel or by editing `_data/team.yml`.
- **Research Keywords**: Can be added/edited in the Admin panel under each person's profile.
- **GitHub Links**: The site automatically links a member's name and photo to their GitHub profile if a link with label "GitHub" is present in their links list.

## Project Structure

- `_data/team.yml`: Contains data for team members (names, bios, keywords, links).
- `_pages/people.html`: The template for the People page.
- `admin/`: Contains configuration for Decap CMS.

## Security & Authentication

- **Local Mode**: When running locally with `npx decap-server`, **no password is required**. The system assumes that if you have access to the local terminal and file system, you are authorized to make changes.
- **Production (GitHub Pages)**: When deployed, you **MUST** configure authentication (e.g., via Netlify Identity or GitHub OAuth). Strangers cannot access the admin panel without logging in.

### Setting up Live Admin (Netlify Identity)

To make the Admin panel work on the live site (`https://korfriend.github.io/admin/`), you need a backend to handle logins. The easiest free way is **Netlify**:

1.  **Sign up for Netlify** (free) and log in.
2.  **"Add new site"** -> **"Import an existing project"**.
3.  Connect to **GitHub** and select your `korfriend.github.io` repository.
4.  **Deploy the site**. (Netlify will mirror your GitHub Pages).
5.  Go to **Site Settings** -> **Identity** -> **Enable Identity**.
6.  Under **Registration preferences**, you can set it to "Invite only" (secure) or "Open".
7.  Go to **Site Settings** -> **Identity** -> **Services** -> **Git Gateway** -> **Enable Git Gateway**.
8.  Now, when you visit your site's Admin panel, you can log in with the email/password you set up in Netlify Identity.

### How it Works (Architecture)

- **Data Storage**: Your data is **NOT** stored in a database. It is stored directly in your **GitHub Repository** (e.g., inside `_data/team.yml`). When you save in the Admin panel, Decap CMS makes a **Git Commit** to your repository behind the scenes.
- **Login Management**: **Netlify Identity** handles the user accounts (email/password). It verifies who you are and then gives the Admin panel permission to write to your GitHub repository (via Git Gateway).
