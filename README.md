# My Blog with mdBook  

Welcome to the **Nefelibata** repository — a static blog generated from Markdown files using **mdBook**.  

The project is fully automated: with a single command, you install dependencies, generate the website, create the RSS feed, configure a custom domain, and publish everything to GitHub Pages (the `gh-pages` branch).  

---  

## 📌 About the Project  

- Static site generator powered by **mdBook**.  
- Direct publishing to the GitHub `gh-pages` branch (no GitHub Actions required).  
- RSS feed generation including post title, date, description, and audio duration (when available).  
- Support for a custom domain configured through `.env`.  
- Helper scripts to:  
  - Rename `.md` files based on their titles.  
  - Automatically update `SUMMARY.md`.  
  - Fix dates inside blockquotes.  
  - Fix line breaks.  
  - Generate a `blog.html` file containing all posts in sequence.  
- Theme, title, author, language, and RSS feed customization through the `.env` file.  

---  

## 🧩 Requirements  

- A Debian/Ubuntu- or Fedora-based operating system (with `apt` or `dnf`).  
- Internet access to download dependencies.  
- Git installed (if not present, it will be installed automatically).  
- A GitHub repository with the `gh-pages` branch configured as the GitHub Pages source.  
- For a custom domain, you must own a registered domain pointing to GitHub.  

---  

# 🚀 Installation  

## 1. Clone the repository  

```bash  
git clone https://github.com/claudeblog/nefelibata.git  
cd nefelibata  
```  

## 2. Create the `.env` file  

Create a file named `.env` with the content below, then adjust the variables to match your project:  

```bash  
# Domain settings  
SITE_URL="https://yourdomain.com"  
DOMAIN="yourdomain.com"  

# Book (mdBook) settings  
BOOK_TITLE="YourDomain.com"  
BOOK_AUTHORS="Claude"  
BOOK_LANGUAGE="en"  

# HTML output settings  
OUTPUT_HTML_DEFAULT_THEME="light"  
OUTPUT_HTML_PREFERRED_DARK_THEME="light"  

# RSS feed settings  
FEED_TITLE="Love the Poem"  
FEED_DESCRIPTION="Poems by Nuvem, palindromes, haiku, and perhaps a podcast someday"  
```  

> **Important:** all variables are required. `install.sh` will not run without this file.  

## 3. Run the installer  

```bash  
chmod +x install.sh  
./install.sh  
```  

The installer automatically performs the following:  

- Reads the `.env` file.  
- Generates `book.toml`.  
- Detects your Linux distribution.  
- Installs:  
  - Git  
  - Curl  
  - Build Essentials  
  - FFmpeg  
- Installs Rust.  
- Installs mdBook.  
- Grants execution permissions to every script inside `scripts/`.  
- Verifies that `ffprobe` is available so audio durations can be included in the RSS feed.  

At the end, the following message will be displayed:  

```text  
🎉 Installation complete!  

Use ./publish.sh to update SUMMARY.md, fix line breaks,  
commit changes, and publish the site.  
```  

---  

# 📝 Customizing the Content  

All Markdown files are located in:  

```text  
src/  
```  

The project already includes:  

- `about.md`  
- `RSS.md`  
- `Cover.md`  

New posts can be created simply by adding `.md` files inside `src/`.  

The `update-summary.sh` script will automatically update `SUMMARY.md`.  

---  

## Theme Configuration  

The following settings are controlled through `.env`:  

- Title  
- Author  
- Language  
- Light theme  
- Dark theme  

After modifying `.env`, run:  

```bash  
./install.sh  
```  

to regenerate `book.toml`.  

---  

# 🔧 Publishing  

Run:  

```bash  
./publish.sh  
```  

The script automatically performs the following:  

1. Loads variables from `.env`.  
2. Renames Markdown files according to their titles (`rename-files.sh`).  
3. Updates `SUMMARY.md`.  
4. Fixes dates inside blockquotes.  
5. Fixes line breaks.  
6. Builds the site with:  

```bash  
mdbook build  
```  

7. Generates `blog.html` containing all posts.  
8. Generates the RSS feed.  
9. Writes the custom domain into the `CNAME` files.  
10. Runs `template.sh` (if it exists).  
11. Commits and pushes everything to GitHub using `git-push.sh`.  

---  

## GitHub Pages  

Configure your repository in:  

```text  
Settings → Pages  
```  

Select:  

```text  
Branch: gh-pages  
```  

After pushing, your website will be available at:  

```text  
https://your-username.github.io/your-repository/  
```  

or at the custom domain defined in `.env`.  

---  

# 🌐 Local Preview  

```bash  
mdbook serve --open  
```  

The server will start at:  

```text  
http://localhost:3000  
```  

Any changes made to your Markdown files will be reflected automatically.  

---  

# 🗂 Project Structure  

```text  
.  
├── book/                  # Generated website  
├── src/                   # Markdown files  
│   ├── about.md  
│   ├── RSS.md  
│   ├── Cover.md  
│   └── ...  
├── scripts/  
│   ├── fix-dates.sh  
│   ├── fix-line-breaks.sh  
│   ├── update-summary.sh  
│   ├── template.sh  
│   ├── rename-files.sh  
│   ├── create-blog.sh  
│   ├── generate-feed.sh  
│   └── git-push.sh  
├── .env  
├── book.toml  
├── install.sh  
├── publish.sh  
└── README.md  
```  

---  

# 🛠 Advanced Customization  

### Themes  

Add custom CSS inside:  

```text  
theme/  
```  

Then update the `book.toml` generation accordingly.  

### RSS Feed  

The `generate-feed.sh` script uses the metadata defined in `.env`.  

To change the feed format, simply edit this script.  

### Plugins  

You can install plugins such as:  

- mdbook-toc  
- mdbook-mermaid  
- Other plugins compatible with mdBook  

Then add them to `book.toml`.  

---  

# ❓ FAQ  

### Can I use another operating system?  

The installer has been tested on Debian, Ubuntu, and Fedora. Other Linux distributions may require adapting the installation commands.  

---  

### Do I need to install Rust manually?  

No.  

`install.sh` installs both Rust and mdBook automatically.  

---  

### How do I add new posts?  

Create a `.md` file inside `src/`.  

The first line should be a Markdown title:  

```md  
# My New Post  
```  

During publishing:  

- the file will be renamed according to its title;  
- it will be automatically added to `SUMMARY.md`.  

---  

### The RSS feed doesn't show audio durations.  

Make sure `ffprobe` is available on your system.  

It is installed together with FFmpeg during the installation process.  

---  

### How do I change the domain?  

Modify:  

```bash  
SITE_URL  
DOMAIN  
```  

in `.env`, then run:  

```bash  
./publish.sh  
```  

---  
&nbsp;<br>​
&nbsp;<br>​
&nbsp;<br>​
&nbsp;<br>​
&nbsp;<br>​
