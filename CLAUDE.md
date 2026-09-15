# Beautiful Minds Social Center — website

This is the website for **Beautiful Minds Social Center, LLC**, an adult day care in
Lakeland, Florida for seniors with early-onset dementia and those who benefit from
daily companionship and activity.

The owner is **Erica**. She is not a developer. She maintains this site herself by
asking Claude for changes in plain English. Write for that: explain what you changed
in ordinary language, avoid jargon, and never leave her mid-task with something broken.

## How this site works

Plain HTML. **There is no build step, no framework, no database and no CMS.** Each page
is a standalone `.html` file that is served exactly as written. Edit the file, publish,
done.

- **7 real pages** — `index`, `about`, `services`, `volunteer`, `tours-and-pricing`,
  `faq`, `contact`
- **2 support pages** — `thanks.html` (shown after a form is sent) and `404.html`
- `assets/` — `css/`, `js/`, `img/`, `fonts/`. Built from a purchased template, so most
  of the CSS and JS is vendor code. **Don't try to tidy it.**
- `netlify.toml` — hosting config: security headers and cache rules
- `robots.txt`, `sitemap.xml` — for search engines

Styling lives in `assets/css/main.css`. The rest of the CSS files are vendor
(Bootstrap, FontAwesome, carousels). jQuery-based; the page markup uses Bootstrap grid
classes (`col-lg-6`, `mb-30`, etc.).

## Publishing

The site is hosted on **Netlify**, connected to this GitHub repository. **Pushing to
the `main` branch publishes the site automatically** — usually live within a minute.

So the full workflow is: edit the files, commit, push. That's the deploy.

Check the deploy actually succeeded before telling Erica it's done.

## Things that will break the site if you get them wrong

**The address must be identical everywhere.** It appears about 20 times across the
pages:

```
1037 South Florida Ave, Ste 130, Lakeland, FL 33803
```

Google uses consistent name/address/phone to rank local businesses. If you change the
address, change **every** instance, including the `LocalBusiness` structured data block
in `index.html` and the Google Maps embed on `contact.html`. Never leave two versions
on the site — that exact problem existed here before and sent families to the wrong
building.

Phone `863-450-4234` and email `contact@beautifulmindssocialcenter.com` likewise appear
on every page and must stay in step.

**The forms are Netlify Forms and are fragile to markup changes.** There are four:

| Form name | Page |
|---|---|
| `contact` | contact.html |
| `homepage-enquiry` | index.html |
| `volunteer` | volunteer.html |
| `tour-request` | tours-and-pricing.html |

Each needs all of: `data-netlify="true"`, a matching hidden `form-name` input, the
`bot-field` honeypot, and a `name` attribute on every input. Netlify detects forms by
scanning the HTML **at deploy time** — so a broken form fails silently and enquiries are
lost with no error anywhere. If you touch a form, submit it afterwards and confirm it
arrives. These forms were dead for months before anyone noticed.

Submissions email `contact@beautifulmindssocialcenter.com` and are also stored in the
Netlify dashboard.

**Wording Erica has specifically chosen. Do not "improve" these:**

- The homepage headline is her slogan: **"Where your family is OUR FAMILY"** — the
  capitals are deliberate.
- The insurance and payment wording on the FAQ page is exact and consequential. It says
  what she accepts and what is under contract. **Never reword it without asking her** —
  families make decisions on it.
- **"Simply Healthcare"** is a company name. Never shorten or alter it.

## Things worth knowing

- Every page must keep its own `<title>` and meta description. They were all identical
  once and it hurt her in search results.
- Phone and email are `tel:` and `mailto:` links. Keep them that way — most visitors are
  on phones and tap to call.
- The contact page map is a **keyless Google Maps iframe embed**. It needs no API key.
  An earlier version loaded the paid Maps API with a key exposed in the page; that was
  removed. Don't reintroduce it.
- Images are compressed. If you add photos, compress them first — page weight is charged
  as bandwidth on the hosting plan.
- The hosting plan has a monthly credit allowance. Batch edits into one push rather than
  publishing after each small change.

## Common requests and where they live

| She asks for | Where |
|---|---|
| Change opening hours | `faq.html` (hours Q), and the structured data in `index.html` |
| Change prices / payment methods | `faq.html` |
| Reword a page | the relevant `.html` file |
| Swap a photo | `assets/img/` — keep the same filename to avoid touching the HTML |
| Add a page | copy an existing page for the header/footer, then add it to the nav on **all** pages and to `sitemap.xml` |
| Change the phone number or address | every page — see above |

Navigation is duplicated in the header and footer of every page. There are no includes
or templates, so a nav change means editing all nine files. Change them all or none.

## Before you tell her it's done

1. The change appears on every page it should
2. Nothing else moved — especially address, phone, email
3. The deploy succeeded
4. If you touched a form, you submitted it and it arrived
