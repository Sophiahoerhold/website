# Publishing the website with GitHub and Netlify

This guide takes you from "folder on my Mac" to "website online" without using the Terminal and without installing Homebrew. It takes about 30 minutes the first time.

**How it works:**

```
Your Mac  ──(GitHub Desktop)──▶  GitHub  ──(automatic)──▶  Netlify  ──▶  your website
 the files                       stores the files            builds and hosts the site
```

You change files on your Mac and send them to GitHub with one click. Netlify notices the change, rebuilds the site and puts it online, usually within a minute. You never have to install Hugo for that: Netlify builds the site itself.

**What you need:**

- A Mac with macOS 12 or newer
- The website folder (the one containing `hugo.toml`, `netlify.toml` and this file)
- An e-mail address
- Both GitHub and Netlify are free for a site like this

---

## Step 1: Create a GitHub account

1. Go to **https://github.com/signup**.
2. Enter your e-mail address, a password and a username. The username is visible to others, e.g. `sophiahoerhold`.
3. Confirm your e-mail address with the code GitHub sends you.
4. If GitHub asks questions about your plans or team, you can skip them. Choose the **Free** plan.

> Recommended: turn on two-factor authentication under *Settings → Password and authentication*. GitHub will ask you to do this sooner or later anyway.

## Step 2: Install GitHub Desktop

GitHub Desktop is a normal Mac app that uploads your files to GitHub. No Terminal needed.

1. Go to **https://desktop.github.com** and click **Download for macOS**.
2. Open the downloaded file in your *Downloads* folder. If it is a `.zip`, double-click it first.
3. Drag **GitHub Desktop** into your **Applications** folder and open it.
4. Click **Sign in to GitHub.com**. Your browser opens; log in and click **Authorize desktop**. Confirm that the browser may open GitHub Desktop.
5. On the "Configure Git" screen, keep your name and e-mail as suggested and click **Finish**.

## Step 3: Put the website folder on GitHub

1. Optional but recommended: move the website folder to a permanent place first, e.g. *Documents* → `website`. Do this **before** the next steps; moving it later confuses GitHub Desktop.
2. In GitHub Desktop, choose **File → Add Local Repository…**
3. Click **Choose…** and select the website folder (the folder that contains `hugo.toml`). Click **Add Repository**.
4. GitHub Desktop says *"This directory does not appear to be a Git repository"*. Click the blue link **create a repository** in that message.
5. In the window that opens:
   - **Name:** e.g. `sophia-hoerhold-website`
   - **Description:** leave empty or write something short
   - **Git ignore:** None
   - **License:** None
   - Click **Create Repository**.
6. Top right, click **Publish repository**.
   - Keep **Keep this code private** checked. Netlify can still read it, but nobody else can see the files.
   - Click **Publish Repository**.

Check: open **https://github.com** in your browser. Your new repository appears on the left. Click it, and you see the files `hugo.toml`, `netlify.toml`, `README.md` and the folders `content`, `data`, `themes`.

## Step 4: Create a Netlify account and connect GitHub

1. Go to **https://app.netlify.com/signup**.
2. Click **Sign up with GitHub**. This uses your GitHub account, so you need no extra password. Click **Authorize Netlify**.
3. Netlify asks a few onboarding questions (what you're building, a team name). Answer briefly or pick anything; nothing here is important. If it offers a plan, choose **Free** (Starter).
4. If Netlify immediately offers to deploy a project, go to step 5 below. Otherwise you land on the dashboard.

## Step 5: Put the website online

1. In Netlify, click **Add new project** (or **Add new site**) → **Import an existing project**.
2. Click **GitHub**. A window opens asking where to install Netlify:
   - Choose your account.
   - Select **Only select repositories**, pick `sophia-hoerhold-website`, and click **Install** (or **Save**).
3. Back in Netlify, click the repository `sophia-hoerhold-website`.
4. Netlify shows the build settings. **You don't need to change anything.** The file `netlify.toml` in the folder already tells Netlify what to do. The fields should show:
   - Build command: `hugo --gc --minify --baseURL $URL`
   - Publish directory: `public`
5. Enter a **project name** if asked, e.g. `sophia-hoerhold`. This becomes the address `sophia-hoerhold.netlify.app`. You can change it later.
6. Click **Deploy**.

The first build takes about one minute. When the status changes to **Published**, click the green link (e.g. `https://sophia-hoerhold.netlify.app`). **The website is online.**

### Change the project name later

In Netlify: your project → **Project configuration** (or **Site configuration**) → **General** → **Project details** → **Change project name**.

## Step 6: Connect your own domain (optional)

If you own a domain like `sophiahoerhold.de` or want to buy one:

1. In Netlify, open your project → **Domain management** → **Add a domain**.
2. Enter the domain and follow the steps.
   - **Domain bought elsewhere** (e.g. IONOS, Strato, All-Inkl, United Domains): Netlify shows you the DNS entries to set. Log in at your domain provider and enter them in the DNS settings. The easiest way is usually to switch to **Netlify DNS** by changing the domain's *nameservers* to the four addresses Netlify shows.
   - **Buy a domain directly in Netlify:** possible from the same screen, then everything is set up automatically.
3. DNS changes can take a few minutes up to 24 hours. Netlify then sets up HTTPS (the lock in the browser) automatically.

You don't need to change `baseURL` in `hugo.toml`. Netlify fills in the correct address on every build.

---

## Making changes after that

Every change follows the same three steps: **edit → commit → push**.

### 1. Edit the files

Open the files in a text editor. Which file controls which part of the page is described in `README.md`.

Recommended free editors:

- **Visual Studio Code**: https://code.visualstudio.com (download, drag into Applications)
- **BBEdit**: https://www.bbedit.com (the free mode is enough)

> **Don't use TextEdit** unless you first switch it to plain text (*Format → Make Plain Text*). Otherwise it may save formatting or "smart quotes" that break the files.

To add images, copy them into `themes/hoerhold/static/img/` (or create a folder `static/img/` in the website folder) and reference them as `/img/filename.jpg`.

### 2. Commit (save a version)

1. Open GitHub Desktop. On the left you see every changed file. Green is new, yellow is changed, red is deleted.
2. Bottom left, in **Summary**, write in a few words what you changed, e.g. `New entry: Tagesgespräch WDR 5`.
3. Click **Commit to main**.

### 3. Push (upload)

Click **Push origin** at the top. Done.

Netlify starts building automatically. After about a minute the change is live. Under **Deploys** in Netlify you can watch the progress.

### Quick edits in the browser

For small text changes you don't even need your Mac:

1. Open your repository on **https://github.com**.
2. Click your way to the file, e.g. `data/kunden.yaml`.
3. Click the **pencil icon** (Edit this file) at the top right.
4. Make the change, then click **Commit changes…** → **Commit changes**.

Netlify rebuilds the site the same way.

> If you edit in the browser, click **Fetch origin** / **Pull origin** in GitHub Desktop before you next edit on your Mac. That way your Mac has the latest files.

---

## Previewing on your own Mac (optional)

If you want to see changes **before** they go online, install Hugo once. No Homebrew needed.

1. Go to **https://github.com/gohugoio/hugo/releases/tag/v0.170.1**.
2. Under **Assets**, download **`hugo_0.170.1_darwin-universal.pkg`**. Click *Show all assets* if you can't see it.
3. Double-click the `.pkg` file and follow the installer.
   - If macOS says the file *cannot be opened because it is from an unidentified developer*: open **System Settings → Privacy & Security**, scroll down, and click **Open Anyway** next to the message about Hugo.
4. Open **Terminal** (via Spotlight: ⌘ + Space, type `Terminal`).
5. Type `cd ` (with a space at the end), drag the website folder from the Finder into the Terminal window, and press Enter.
6. Type `hugo server` and press Enter.
7. Open **http://localhost:1313** in your browser. The page updates every time you save a file.
8. To stop it, click into the Terminal window and press **Ctrl + C**.

Hugo writes a folder `public/` when you build. It is excluded via `.gitignore` and won't be uploaded, so that's fine.

---

## When something goes wrong

**The website doesn't change after pushing.**
In Netlify, open **Deploys**. The latest entry should say *Published*. If it says *Failed*, click it and scroll to the red lines in the log. They usually name the file and line with the problem.

**Common causes of a failed build:**

- **Front matter broken**: a missing `---`, or a value with a colon that isn't in quotes. Correct: `title: "Moderation: Podium"`.
- **YAML indentation** in `data/*.yaml`: entries must start with `- ` and the lines under them must be indented with exactly two spaces. Don't use tabs.
- **Date format** in `data/termine.yaml` must be `2027-06-12`.

To undo the last change: in GitHub Desktop, go to **History**, right-click the last commit → **Revert changes in commit**, then **Push origin**.

**An image doesn't show up.**
Check the spelling. Upper and lower case matter online: `Foto.JPG` and `foto.jpg` are different files. Easiest is to use only lowercase letters, no spaces and no umlauts in file names.

**GitHub Desktop says "Authentication failed".**
*GitHub Desktop → Settings → Accounts*: sign out and sign in again.

**Netlify shows a "Page not found".**
Wait a minute after the first deploy and reload. If it persists, check under *Project configuration → Build & deploy* that the publish directory is `public`.

---

## Privacy note (Germany)

Netlify is a US company. For a German website, mention the hosting in the privacy policy (`content/datenschutz.md`): Netlify processes visitors' IP addresses to deliver the website. Netlify offers a data processing agreement (DPA, *Auftragsverarbeitungsvertrag*), which you can accept in your Netlify account under the team settings. The site itself sets no cookies and loads no external fonts or scripts. Have the privacy policy and imprint checked before you share the link publicly.
