README - No Rush No Fuss Tours (Multi-page template)

What's included:
- index.html (home)
- tours.html (Airport pickup/dropoff, city tours, and excursions)
- about.html ()
- booking.html (<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Booking — No Rush No Fuss Tours</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
<header class="site-header">
  <div class="container">
    <a class="logo" href="index.html">No Rush No Fuss Tours</a>
    <nav class="nav" aria-label="Main">
      <button id="nav-toggle-4" aria-expanded="false" aria-controls="nav-list-4">Menu</button>
      <ul id="nav-list-4" class="nav-list">
        <li><a href="index.html">Home</a></li>
        <li><a href="tours.html">Tours</a></li>
        <li><a href="about.html">About</a></li>
        <li><a href="booking.html">Booking</a></li>
        <li><a href="contact.html">Contact</a></li>
      </ul>
    </nav>
  </div>
</header>

<main class="container">
  <h1>Booking</h1>
  <p>Fill out the form below to request a booking. You will receive a confirmation email after submission.</p>

  <!-- Booking Form -->
  <form id="booking-form" action="https://formspree.io/f/xyz123" method="POST">
    <label for="b-name">Full Name</label>
    <input id="b-name" name="name" type="text" required>

    <label for="b-email">Email</label>
    <input id="b-email" name="email" type="email" required>

    <label for="b-phone">Phone</label>
    <input id="b-phone" name="phone" type="tel">

    <label for="b-date">Preferred Date</label>
    <input id="b-date" name="date" type="date" required>

    <label for="b-tour">Select Tour</label>
    <select id="b-tour" name="tour" required>
      <option value="">-- choose a tour --</option>
      <option value="dunns-river">Dunn's River Falls & Beach</option>
      <option value="blue-mountains">Blue Mountains Coffee Tour</option>
      <option value="martha-brae">Martha Brae River Rafting</option>
      <option value="custom">Custom / Private Tour</option>
    </select>

    <label for="b-people">Number of People</label>
    <input id="b-people" name="people" type="number" min="1" value="2" required>

    <label for="b-message">Special Requests / Message</label>
    <textarea id="b-message" name="message" rows="4"></textarea>

    <button type="submit">Request Booking</button>
    <div id="booking-status" role="status" aria-live="polite"></div>
  </form>
</main>

<footer class="site-footer">
  <div class="container">&copy; <span id="year-4"></span> No Rush No Fuss Tours</div>
</footer>

<script src="script.js"></script>
</body>
</html>)
- contact.html (contact form)
- styles.css (shared stylesheet)
- script.js (shared JS)
- README.txt (this file)

Forms:
- Both booking and contact forms are configured to POST to Formspree using a placeholder endpoint (https://formspree.io/f/maypkwpl).
- To use Formspree: create a free Formspree form, get your endpoint, and replace the `action` attribute in booking.html and contact.html.
- Quick alternative: replace form action with `mailto:you@yourdomain.com` (opens email client) — less reliable.
- Google Sheets option: see below for a Google Apps Script example to capture submissions to a sheet (requires a Google account & a bit of setup).

Deploying (simple methods):
1) Netlify (recommended for non-developers)
   - Go to netlify.com, sign up, and drag-and-drop the extracted folder into the Sites area.
   - Netlify will upload and give you a live URL (you can change the site name to something like norushnofusstours).

2) GitHub Pages
   - Create a new GitHub repo, push these files (root of the repo), then in Settings -> Pages set source to main branch / root.
   - Your site will be at https://<yourusername>.github.io/<repo-name>

3) Vercel — similar to Netlify; connect a Git repo and deploy.

Customizations you might want:
- Replace placeholder images (picsum.photos) with your photos. Optimize sizes for web.
- Update phone/email and add social media links.
- Add pricing, terms, cancellation policy pages if needed.

Google Sheets capture (optional)
1. Create a Google Sheet, open Extensions -> Apps Script and paste a script like below as Code.gs:
```javascript
function doPost(e){
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var data = JSON.parse(e.postData.contents);
  sheet.appendRow([new Date(), data.name || '', data.email || '', data.phone || '', data.date || '', data.tour || '', data.people || '', data.message || '']);
  return ContentService.createTextOutput(JSON.stringify({result:'success'})).setMimeType(ContentService.MimeType.JSON);
}
```
2. Deploy -> New deployment -> Select "Web app", set access to "Anyone", and deploy. Copy the web app URL.
3. In the form, either change the `action` to the web app URL and submit as JSON via JS, or use a simple fetch wrapper to post the form fields as JSON.

Need help deploying?
Tell me which host you prefer (Netlify, GitHub Pages, Vercel) and I will give a step-by-step guide tailored to that service — and I can update the files (e.g., set a custom domain) before you deploy.

If you'd like, I can also:
- Replace the Formspree placeholder endpoint with a working one (I can't create it for you, but I can show the exact steps).
- Add a simple admin CSV download for submissions saved to Google Sheets.

---
Enjoy! Reply if you want color changes, logo, or I should upload this as a ZIP for you to download.
