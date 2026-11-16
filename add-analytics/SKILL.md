---
name: add-analytics
description: Adds website analytics (visitor counts) to a project with GoatCounter, the privacy-friendly way our team uses, with a private dashboard for each project. Use this whenever someone says things like "add analytics", "count visitors", "how many people use our site?", "track page views", "add Google Analytics", "add GoatCounter", "see our visitor numbers", or "set up our dashboard".
---
# Add analytics

**Analytics** counts how many people visit a website and which pages they use, so a team can see
what to make better. Kids use our sites, so we use **GoatCounter**: it uses no cookies, doesn't save
anyone's IP address, and only keeps totals. Never use Google Analytics or other tools with cookies.

Each project gets its **own** GoatCounter site, so its numbers stay separate. Only a grown-up has a
GoatCounter login. Each team sees just its own project's dashboard, through a secret, view-only link.

## Steps
1. **Check first.** Search the project for `goatcounter`, `gtag`, and `googletagmanager`. If
   GoatCounter is already there, stop and say so. If Google Analytics is there, this job replaces it.
2. **Make sure it's planned.** Analytics is a new feature, so it needs a plan in `requirements.md`
   first (see `skills/shared/plan-a-feature/SKILL.md`), unless the plan is already there.
3. **Ask a grown-up for the site code.** It looks like `wizkidz-<project>`. If there isn't one yet,
   give the grown-up these steps:
   - In GoatCounter, open Settings → Sites and add a site with the code `wizkidz-<project>`.
   - In that site's settings, set who can see the dashboard to **Secret token**, and pick a token.
   - Give the team this link: `https://wizkidz-<project>.goatcounter.com/?access-token=<token>`.
4. **Add `analytics.js`** next to the project's other code (see "Where new features go" in
   `AGENTS.md`). Use the site code from step 3 in the comment:
   ```js
   // Website analytics with GoatCounter (site "wizkidz-<project>"). No cookies, and only the
   // page's address is sent. See the privacy policy.
   window.goatcounter = { no_onload: true };   // we count each page ourselves, below
   function countPage() {
     const visit = { path: location.pathname + location.hash, title: document.title };
     let tries = 0;   // GoatCounter's script loads in the background, so wait for it (up to 10 s)
     const send = () => {
       if (window.goatcounter.count) window.goatcounter.count(visit);
       else if (++tries < 50) setTimeout(send, 200);
     };
     send();
   }
   countPage();
   window.addEventListener("hashchange", countPage);   // for sites with screens like #home, #map
   ```
5. **Add two lines inside `<head>` on every HTML page**, in this order (fix the path to `analytics.js`):
   ```html
   <script src="analytics.js"></script>
   <script data-goatcounter="https://wizkidz-<project>.goatcounter.com/count" async src="https://gc.zgo.at/count.js"></script>
   ```
6. **Update the privacy policy**, if the project has one, and ask a grown-up to read it. Say that
   we use GoatCounter, that it counts visits, pages, browsers, screen sizes, countries, and which
   site sent people here, that it uses no cookies and doesn't save IP addresses, and that it's not
   used for ads. If there's no privacy policy, tell a grown-up the project needs one.
7. **Add `analytics.js` to "Where things are"** in `AGENTS.md`.

## Check that it worked
1. Run the site (see *Run it* in `AGENTS.md`) and open the browser's developer tools (F12).
   - **Console:** no red errors.
   - **Application → Cookies:** empty. No cookies means no tracking.
   - **Network:** `count.js` loaded. GoatCounter ignores visits from your own computer
     (`localhost`), so nothing shows on the dashboard yet. That's expected.
2. After the grown-up merges, open the live site, click around, then open the secret dashboard
   link. Each page should show up within a minute.

## Be careful
- **The access token is a secret.** Never put it in any file, commit, issue, or pull request. The
  site code (`wizkidz-<project>`) is fine to share: every visitor's browser sees it anyway.
- **Only send the page's address.** Never send names, photos, locations, or anything a person
  types. That's why the code leaves out `location.search` (the `?...` part), which can hold typed text.
- **Don't turn on `allow_local`.** It would count our own tests and mess up the real numbers.
- **One site per project.** Don't reuse another team's site code: their dashboard would get your
  visits.
- If a team's secret link leaks, a grown-up changes that site's token. Only that project's link
  stops working.
