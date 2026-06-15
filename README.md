# Southbourne School of English — Full Website

Complete static site mirroring the original southbourneschool.co.uk URL structure
to preserve Google rankings. 36 pages + blog.

## URL structure (matches the live site exactly)

```
/                                                            Home
/english-courses/                                            Courses hub
/english-courses/guide-to-levels/                            CEFR guide
/english-courses/how-to-book-your-english-course/            Booking & prices
/english-courses/adult-language-courses/                     Adult hub
/english-courses/adult-language-courses/general-intensive/
/english-courses/adult-language-courses/one-to-one-english/
/english-courses/adult-language-courses/summer-vacation-courses/
/english-courses/adult-language-courses/cambridge-examination-courses/
/english-courses/junior-language-courses/                    Junior hub
/english-courses/junior-language-courses/summer-courses/
/english-courses/junior-language-courses/year-round-group-courses/
/studying-in-bournemouth/                                    + 6 sub-pages
/about/                                                      + 8 sub-pages incl. /about/gallery/
/blog/                                                       + 3 starter posts
/agents/  /hosting-students/  /contact-us/  /request-a-quote/
```

## CRITICAL: deployment requirements for SEO

1. **Custom domain required.** All internal links are root-relative (e.g. `/about/faqs/`).
   The site MUST be served at the domain root — either:
   - GitHub Pages with the custom domain `southbourneschool.co.uk` connected, or
   - a user/organisation site (`username.github.io` repo)
   It will NOT work correctly at `username.github.io/repo-name/`.

2. **Add a CNAME file** containing `southbourneschool.co.uk` (GitHub creates this when
   you set the custom domain in Settings → Pages).

3. **URL parity is preserved** for all pages in the current site navigation, so existing
   Google rankings carry over. The alternate URL `/english-courses/adult-language-courses/examination-courses/`
   (used inconsistently on the old site) redirects to the canonical Cambridge page.

4. **Blog**: the 3 included posts are NEW starter posts at new URLs (no ranking risk).
   Your EXISTING blog posts on WordPress have their own URLs — before switching DNS, list them
   (Search Console → Pages) and recreate each at the identical slug, or add redirects,
   or rankings for those posts will be lost.

5. **Submit `sitemap.xml`** in Google Search Console after going live.

## Also note

- Team page uses role descriptions, not names — add real names/photos before launch.
- School Policies page links are placeholders — upload your policy PDFs and link them.
- Review cards marked "Replace with a real Google review" need genuine review text.
- Forms: add your reCAPTCHA secret key in Formspree; whitelist the domain in reCAPTCHA admin.
