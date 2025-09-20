README - No Rush No Fuss Tours (Multi-page template)

What's included:
- index.html (home)
- tours.html (list of tours)
- about.html (company info)
- booking.html (booking request form)
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
