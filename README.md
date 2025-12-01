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
