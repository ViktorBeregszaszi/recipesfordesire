# Recipes for Desire, workshop site

A single-page, static site. No build step, no framework, no database. Edit
`index.html` in any text editor and the site changes.

```
index.html      the whole page, including all styling
images/         six photographs and the infographic
CNAME           tells GitHub which domain to serve
robots.txt      keeps search engines out
README.md       this file, not published
```

---

## Part 1. Get the site online (about 20 minutes)

**1. Make a GitHub account** at github.com if you do not have one.

**2. Create a repository.** Click the `+` in the top right, choose
*New repository*. Name it `recipesfordesire`. Set it to **Public**, because
GitHub Pages needs public on a free account. Do not tick "Add a README". Click
*Create repository*.

**3. Upload the files.** On the empty repository page, click
*uploading an existing file*. Drag in `index.html`, `CNAME`, `robots.txt`,
`README.md`, **and the whole `images` folder**. Wait for all seven items to
appear in the list, then click *Commit changes*.

> If dragging the folder does not work in your browser, drag the six image
> files in on their own first, but put them inside a folder called `images`
> using the *Add file, Create new file* trick: type `images/placeholder.txt`
> as the filename, commit, then upload the photos into that folder.

**4. Turn on Pages.** Go to *Settings*, then *Pages* in the left sidebar.
Under *Source* choose **Deploy from a branch**. Branch: `main`, folder: `/ (root)`.
Click *Save*.

Wait two or three minutes. The site is now live at
`https://YOURUSERNAME.github.io/recipesfordesire/`.

**Check it works at that address before doing anything with the domain.**

---

## Part 2. Point the domain at it (Porkbun)

**1. In Porkbun**, open *Domain Management*, find recipesfordesire.com, click
*DNS*. Look for **Quick DNS Config** and pick the **GitHub Pages** preset. That
adds the right records for you.

If the preset is not there, add these by hand:

| Type | Host | Answer |
|---|---|---|
| A | (leave blank) | 185.199.108.153 |
| A | (leave blank) | 185.199.109.153 |
| A | (leave blank) | 185.199.110.153 |
| A | (leave blank) | 185.199.111.153 |
| CNAME | www | YOURUSERNAME.github.io |

**2. Back in GitHub**, *Settings*, *Pages*, *Custom domain*: type
`recipesfordesire.com` and save. The `CNAME` file in the repo already contains
this, so GitHub should pick it up on its own.

**3. Wait.** DNS takes anything from ten minutes to a few hours. When GitHub
shows a green tick next to the domain, tick **Enforce HTTPS**.

Do this part a day before you need the link, not on the morning it is due.

---

## Part 3. Make the enquiry form work

The form will not send anything until you connect it. Right now it points at a
placeholder.

**1.** Sign up at **formspree.io** with the free plan (50 submissions a month,
far more than you need).

**2.** Create a new form. Set the destination to your Gmail. Formspree gives
you an endpoint that looks like `https://formspree.io/f/xayzbwqr`.

**3.** In `index.html`, find this line (around line 437):

```html
<form class="form reveal" action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
```

Replace `YOUR_FORM_ID` with the code from your Formspree form. Commit the change.

**4.** Send yourself a test enquiry. The first submission asks you to confirm
your email address, so do this before you send the link to anyone.

The form already includes a hidden anti-spam field, so you should not get bot
submissions.

**Note on where the data goes.** Formspree is a US company. For a handful of
festival enquiries with a consent checkbox and a plain-English notice, which
the page has, this is proportionate. If you want the data to stay in the EU,
Brevo can host an equivalent form and I can swap it in. Say the word.

---

## Part 4. The email address

Porkbun gives you **20 free forwarding addresses** with the domain. In *Domain
Management*, click the envelope icon, then create a forward from
`hello@recipesfordesire.com` to your Gmail.

Do **not** set up Gmail's "send mail as" for this address. That is what breaks
deliverability. Receive on the domain address, reply from Gmail.

---

## Editing the site later

Everything is in `index.html`. Click the file on GitHub, click the pencil icon,
edit, commit. The site updates in about a minute.

- **Colours and fonts** are all in the `:root{ }` block near the top of the
  file. Change a hex value there and it changes everywhere. Hand this block to
  a designer if you get one.
- **The logo.** When you have the SVG, put it in `images/` and replace the
  `<h1>Recipes for Desire</h1>` line in the hero with an `<img>` tag. Send it
  to me and I will do it.
- **Making the page findable.** When you eventually want Google to index it,
  delete the `<meta name="robots" content="noindex, nofollow">` line and change
  `robots.txt` to allow crawling. Until then the page works perfectly for
  anyone you send the link to, and does not surface in a search for your name.

---

## Things worth knowing

**The fonts come from Google.** That means a visitor's IP address reaches
Google's servers. A German court decided in 2022 that this needs consent, and
the safest fix is to host the font files yourself. It is a real but small
issue at this scale. Say the word and I will convert the site to self-hosted
fonts, which also removes any question of a cookie banner.

**The infographic says "Favorite Ingredients"** in panel 2. American spelling.
Everything else on the site and the one-pager is British. Worth fixing when you
next open the graphic.

**No analytics are installed.** No cookies are set by the site itself. That is
why there is no cookie banner and no privacy page.
