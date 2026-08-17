# Southbourne School of English — Full Website

Complete static site mirroring the southbourneschool.co.uk URL structure to preserve
Google rankings. 49 pages + 1 redirect stub.

**Currently deployed:** GitHub Pages at
`https://joshuajgarner.github.io/southbourneschoolofenglish/`
**Target:** Fasthosts shared hosting serving `southbourneschool.co.uk`

## URL structure

```
/                                                            Home
/course-calculator/                                          Dual-year 2026/2027 price calculator
/english-courses/                                            Courses hub
/english-courses/guide-to-levels/                            CEFR guide
/english-courses/how-to-book-your-english-course/            Booking & prices
/english-courses/adult-language-courses/                     Adult hub
    general-intensive/
    one-to-one-english/
    summer-vacation-courses/
    cambridge-examination-courses/
    over-30s-executive-english/
    english-for-content-creators/
    english-to-prepare-for-university/
    examination-courses/                                     Redirect stub -> cambridge-examination-courses
/english-courses/junior-language-courses/                    Junior hub
    summer-courses/
    year-round-group-courses/
/studying-in-bournemouth/                                    Hub
    travelling-to-britain/
    school-activities/
    our-location/
    accommodation-welfare/  + homestay/  + guesthouses-hotels/
/about/                                                      Hub
    school-facilities/  gallery/  our-team/  join-our-team/
    testimonials-accreditations/  school-policies/
    visa-information/  faqs/
/blog/                                                       + 9 posts
/agents/  /hosting-students/  /contact-us/  /request-a-quote/
/privacy-policy/  /terms-conditions/  /search/
```

## CRITICAL: deployment requirements

### While on GitHub Pages (current)

All internal links, image paths and the search index carry the
`/southbourneschoolofenglish/` prefix (196 occurrences on the homepage alone).
This is what makes the site work at the project-page URL. `.nojekyll` is present so
GitHub serves the files as-is.

### At the Fasthosts cutover (five phases)

1. **Strip the path prefix.** Remove `/southbourneschoolofenglish/` from every internal
   link, image `src`, `data-full`, `sitemap.xml`, `robots.txt` and the `PAGES` search
   array in all HTML files. Root-relative links (`/about/faqs/`) only work at a domain
   root. Doing this while still on GitHub Pages will break the site.
2. **Upload** the site to `htdocs` on Fasthosts.
3. **Test** on the Fasthosts preview URL before touching DNS.
4. **DNS cutover:** update the A record and the `www` CNAME.
5. **Post-cutover:** enforce HTTPS, whitelist the domain in reCAPTCHA admin and
   Formspree, resubmit `sitemap.xml` in Google Search Console.

Cancel WordPress hosting only after the new site has been confirmed stable.

### SEO notes

- **URL parity is preserved** for every page in the current navigation, so existing
  rankings carry over. `/english-courses/adult-language-courses/examination-courses/`
  (used inconsistently on the old site) redirects to the canonical Cambridge page.
- **Blog:** the 9 posts here are at new or recreated URLs. Before switching DNS, list
  the existing WordPress posts (Search Console → Pages) and confirm each is recreated
  at an identical slug or redirected, or rankings for those posts will be lost.
- `sitemap.xml` currently lists 41 URLs and `robots.txt` points at
  `https://southbourneschool.co.uk/sitemap.xml` — correct for the target domain, not
  for GitHub Pages.

## Outstanding before launch

- **School Policies:** all five policy cards show "PDF coming soon". Upload the PDFs
  and link them.
- **Reviews — three gaps.** Every review card now carries a real, named review. Three
  audiences still lack a review in their own voice, and currently show named student
  reviews instead:
  - homestay hosts (`/hosting-students/`, `/studying-in-bournemouth/accommodation-welfare/homestay/`)
  - education agents (`/agents/`)
  - parents of junior students (`/english-courses/junior-language-courses/*`)

  Longer term, a live Google reviews widget (Trustindex is already in use on the
  WordPress site) would keep names and avatars current automatically.
- **Forms:** Formspree endpoint `xdavlbvq`; reCAPTCHA v3 is lazy-loaded on form focus.
  Add the reCAPTCHA secret key in Formspree and whitelist the live domain in reCAPTCHA
  admin at cutover.
- **Southampton airport** was removed from Travelling to Britain but is still offered
  as a paid transfer in the course calculator, the Request a Quote dropdown and the
  Over 30s Executive English page. Decide whether those should go too.

## Maintenance notes

- **Never replace header/nav blocks wholesale** — add alongside the existing structure.
  Wholesale replacement has broken multiple pages before.
- **All prices shown publicly are gross.** Net and agent-commission figures must never
  appear on public pages.
- **Search index:** every HTML file embeds its own copy of the `PAGES` array, which
  drives both the dropdown search and the full results page. There is no rebuild
  script — edits must be applied to every file, usually with a Python glob script.
- **Site-wide changes** should be made with idempotent Python scripts using assertion
  guards (`assert h.count(old) == 1`) before writing, to catch silent multi-match errors.
- **Div counts are imbalanced by one** in most HTML files, including untouched ones.
  This is a pre-existing template quirk, not a symptom of a broken edit.
- **CSS scoping:** avoid scoping under `#calcApp` — it previously captured `:root`
  variables and broke the calculator.
- Keep the local repo outside OneDrive (`C:\repos\`) to avoid Unlink errors during
  git operations.

## Design system

- CSS variables: `--navy` #0E2A52, `--sky` #29ABE2, `--leaf` (green), `--sun`/`--gold`
  (yellow), `--foam` (pale blue background), `--line` (border)
- Fonts: Bricolage Grotesque (display), Albert Sans (body)
- Junior pages use the `theme-junior` body class (green theme)
- Key structures: `.page-hero` with breadcrumbs, eyebrow, waves SVG and CTA buttons;
  `.card-grid` / `.card`; `.gal` masonry photo grid; `.quote-grid` / `.quote` reviews;
  mobile menu via `#mobileOverlay`, `#mobilePanel` and the `.mob-toggle` /
  `data-target` pattern
