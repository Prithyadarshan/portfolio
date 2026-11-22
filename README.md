# Prithyadarshan T – Portfolio Website
 
A responsive personal portfolio for **Prithyadarshan T**, a final-year Computer Science and Engineering (AI & ML) student at Saranathan College of Engineering, Tiruchirappalli. It presents internships, projects, certifications, technical presentations and achievements in one clean page, and can generate a text-based resume PDF from the same content.
 
The whole site is a single HTML file with its own CSS and JavaScript. There is no framework and no build step, so it can be opened locally or hosted for free in a few minutes.
 
## Project goals
 
This project explores how a recruiter-friendly portfolio can be kept simple, fast and easy to update. It demonstrates:
 
- A clear page sequence: About me, then Education, followed by skills, experience, projects and credentials.
- Content stored in plain JavaScript arrays, so one edit updates both the website and the resume PDF.
- Filters that let visitors narrow down projects and certifications by category.
- A resume PDF created in the browser as selectable text, which job-application systems can read.
- A layout that works on phones, tablets and desktops, and follows the visitor's light or dark setting.
## What the website shows
 
| Section | Contents |
| --- | --- |
| Hero | Profile photo, name, role, career objective, contact buttons, resume PDF button |
| About me | Three short paragraphs on background, skills and presentations |
| Education | B.E. CSE (AI & ML), HSC and SSLC, with dates and scores |
| Technical skills | 6 skill cards: AI/ML/NLP, Languages, Data & analytics, Web & database, Core skills, Tools & platforms |
| Experience | 3 internships: Skill Set Go EduTech, SASTRA University, InternPe |
| Projects | 15 projects with dates, descriptions and technology tags |
| Certifications | 20 certifications with issuer and date |
| Technical presentations | 4 papers and posters at colleges and universities |
| Achievements | 7 hackathons, badges and contests |
| Languages known | Tamil and English |
| Contact | Email, phone, LinkedIn and GitHub |
 
The Skill Set Go EduTech card also links to the four task repositories on GitHub.
 
## Design approach
 
The page uses a light theme with soft blue and lavender tints and black text. Cards have colored top borders in blue, teal, violet and amber. Colors are CSS variables at the top of the file, so the look can be changed in one place.
 
| Variable | Used for | Default |
| --- | --- | --- |
| `--bg` | Page background | `#f6f8ff` |
| `--alt` | Alternate section background | `#e7eeff` |
| `--ink` | Main text | `#0d0d12` |
| `--acc` | Main accent (blue) | `#1f4fd8` |
| `--c2` | Teal accent | `#0e9f8e` |
| `--c3` | Violet accent | `#7c3aed` |
| `--c4` | Amber accent | `#f59e0b` |
 
Fonts are Sora for headings and Source Sans 3 for body text, loaded from Google Fonts with system fonts as a fallback.
 
## Project files
 
```
portfolio-v2.html   # The whole website: HTML, CSS and JavaScript in one file
README.md           # This guide
```
 
Rename `portfolio-v2.html` to `index.html` before hosting it.
 
## Content arrays
 
The repeating content lives in JavaScript arrays near the bottom of the file. Each item is a list in a fixed order.
 
| Array | Section | Item format |
| --- | --- | --- |
| `S` | Technical skills | `[title, "skill 1,skill 2,skill 3"]` |
| `E` | Experience | `[role, company, dates, place, [points], [[label, url], ...]]` (links are optional) |
| `P` | Projects | `[category, title, dates, description, "tag 1,tag 2"]` |
| `C` | Certifications | `[name, issuer, date, category]` |
| `T` | Presentations | `[type and date, title, venue]` |
| `A` | Achievements | `[title, date or label, description]` |
 
Category codes:
 
| Where | Code | Filter name |
| --- | --- | --- |
| Projects | `ai` | AI & ML |
| Projects | `cv` | Vision & NLP |
| Projects | `web` | Software & web |
| Certifications | `ai` | AI & data |
| Certifications | `cl` | Cloud & security |
| Certifications | `cd` | Coding |
| Certifications | `ev` | Events |
 
Write `&` as `&amp;` inside these arrays, because the text is inserted into the page as HTML. The resume PDF converts it back automatically.
 
The About me paragraphs, education, contact details and languages are written directly in the HTML. If you change them, update the matching lines inside the `mk()` function so the resume PDF stays the same.
 
## How to add or change something
 
1. Open the file in a code editor such as VS Code.
2. Find the array for that section (for example `P` for projects).
3. Copy an existing item, paste it, and change the text. Keep the commas and quotes.
4. Save the file and refresh the browser.
5. Check the section, its filter button and the resume PDF.
## Resume PDF
 
The button below the name creates an A4 PDF with the `mk()` function and the jsPDF library. The PDF contains the contact details, career objective, education, skills, experience (with task repository links), all projects with tags, certifications, presentations, achievements and languages. Pages break automatically. The profile photo and colors are left out on purpose, so the file stays simple and readable by job-application systems.
 
Inside Claude the file is saved through Claude's download feature. If you host the page on your own site, the button shows "Download unavailable here" until you replace the save step with a normal browser download. Find this line:
 
```js
return dl.save({filename:"Prithyadarshan_T_Resume.pdf",data:blob})
```
 
and in the same click handler, finish with this instead:
 
```js
var a=document.createElement("a");
a.href=URL.createObjectURL(blob);
a.download="Prithyadarshan_T_Resume.pdf";
a.click();
```
 
The function `rz()` is an unused leftover from an earlier version and can be deleted.
 
## Profile photo
 
The photo is embedded in the `<img class="ph" ...>` tag as a base64 image, which is why the file is large. To use a normal image file, place it in an `images/` folder and change the tag to:
 
```html
<img class="ph" src="images/photo.jpg" alt="Portrait of Prithyadarshan T" width="360" height="360">
```
 
## Run locally
 
1. Download `portfolio-v2.html`.
2. Double-click it to open it in a browser.
3. Stay online for the first run, because the fonts and the jsPDF library load from the internet.
## Deploy for free
 
**GitHub Pages**
 
1. Create a repository and upload `index.html` and `README.md`.
2. Open Settings, then Pages, choose the `main` branch and the root folder, and save.
3. The site appears at `https://<your-username>.github.io/<repository-name>/`.
**Netlify**
 
1. Open app.netlify.com/drop.
2. Drag and drop the folder that contains `index.html`.
## Troubleshooting
 
- **A section is empty or the filters do not work:** a comma, bracket or quote is probably missing in one of the arrays. Open the browser console (F12) to see the error line.
- **A project or certification disappears when filtering:** check that its category code is one of the codes in the table above.
- **Fonts look different:** the Google Fonts request failed, so the page is using system fonts. It still works.
- **Resume PDF button shows "Download unavailable here":** the page is running outside Claude. Use the browser download snippet in the Resume PDF section.
- **Resume PDF shows a strange character:** the PDF uses a standard font, so replace unusual symbols with plain text in the arrays.
- **The file is slow to open in an editor:** the embedded photo is large. Switch to an image file as shown above.
## Limitations
 
- The content is static. Dates, scores and descriptions must be updated by hand.
- The contact area uses direct email, phone and profile links. It has no contact form.
- Task and project descriptions are summaries. Add GitHub links or screenshots for more detail.
- The page needs an internet connection for fonts and for the PDF library.
## Possible extensions
 
- Add GitHub or live-demo links and screenshots to each project.
- Add a short blog or notes section on research work.
- Add a contact form using a form service.
- Add a manual light and dark theme switch.
- Add a downloadable ready-made PDF resume as a second option.
- Add basic analytics to see which sections visitors read.
## Main technologies
 
- HTML5 and CSS (custom properties)
- Vanilla JavaScript
- jsPDF 2.5.1 (loaded from cdnjs)
- Google Fonts: Sora and Source Sans 3
## Contact
 
- Email: prithyadarshant@gmail.com
- LinkedIn: https://linkedin.com/in/prithyadarshan-thiyagarajan-379a4b2a3
- GitHub: https://github.com/prithyadarshan
---
 © 2026 Prithyadarshan T. All rights reserved.
 
