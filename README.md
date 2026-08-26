# lunaplum.com

Static site for the Lunaplum studio and its apps. No build step, no framework,
no JavaScript. Edit the HTML, push, done.

```
/                  studio page, deliberately plain
/aurava/           Aurava waitlist page
/aurava/privacy    the Privacy Policy pasted into App Store Connect
```

App two gets `/nextapp/`. DNS is touched once, ever.

## Namecheap DNS, the one manual step

Namecheap dashboard > Domain List > lunaplum.com > **Manage** > **Advanced DNS** >
Host Records. Delete the parking page records Namecheap added, then add these five.
Verified against GitHub's own documentation on 27 August 2026.

| Type | Host | Value | TTL |
|---|---|---|---|
| A Record | `@` | `185.199.108.153` | Automatic |
| A Record | `@` | `185.199.109.153` | Automatic |
| A Record | `@` | `185.199.110.153` | Automatic |
| A Record | `@` | `185.199.111.153` | Automatic |
| CNAME Record | `www` | `kaganduran.github.io.` | Automatic |

Delete any `URL Redirect Record` or `CNAME` on `@` or `www` that Namecheap created,
or the A records will not take effect.

Propagation is usually minutes and can take up to 24 hours. Check with:

```sh
dig +short lunaplum.com
curl -sI https://lunaplum.com | head -1
```

Once it resolves, go to the repo's **Settings > Pages** and tick **Enforce HTTPS**.
That checkbox stays greyed out until GitHub has issued the certificate, which needs
the DNS to be live first, so it is the last step rather than the first.

Email forwarding for `hello@lunaplum.com` is set up in the same Namecheap panel, under
**Domain > Redirect Email**. It coexists with the records above.

## Fonts

Bodoni Moda and Archivo are self-hosted in `assets/fonts/` as latin-subset variable
woff2, 82 KB for the pair. They are deliberately not loaded from Google's CDN, so a
visitor to this site contacts no third party at all. The Privacy Policy says so, so
if you ever switch to a CDN, section 13 has to change with it.

## Structure

```
index.html                  studio
aurava/index.html           waitlist
aurava/privacy/index.html   policy
styles.css                  everything, one file
assets/fonts/               two woff2
assets/favicon.svg
CNAME                       lunaplum.com
.nojekyll                   skip Jekyll, serve the files as they are
APP-PRIVACY-LABELS.md       what to tick in App Store Connect
TODO.md                     open items
```

## Design notes

The palette comes from the fruit the studio is named after: a dark blue-purple skin
`#2A1B33`, the pale waxy bloom that sits on it `#E8E4EE`, and the amber flesh near the
stone `#C08A2E`. Marketing pages are the skin side and run dark. Documents are the cut
side and run pale. Amber is a mark, never text on a light ground, because it does not
carry enough contrast there.

The repeated line on `/aurava/` is the signature. It is the 369 practice the app
implements, set as type. It is `aria-hidden` so a screen reader hears the sentence once,
and its fade-in is dropped entirely under `prefers-reduced-motion`.

## Copy rules

Project-wide. No em-dashes. No "it is not X, it is Y" constructions. No chatbot tone,
no generic wellness filler. Hero copy names what changes for her, never a feature count.
A manifestation app that promises outcomes is both dishonest and an App Review risk, so
the copy sells the practice and never the result.

## Open items

Tracked in `TODO.md` and `APP-PRIVACY-LABELS.md`, both deliberately left out of this
public repo and kept in the working directory only. See `.gitignore` for why.
