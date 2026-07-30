# IO&E Medical Event Hub

A GitHub-ready, browser-based prototype for tracking **Y-90, DC Bead, cryoablation, and other medical events** from commercial intake through Medical review, governance, execution, and close-out.

The application includes reusable physician records, event-format details, IRF tracking, and a presentation-review workflow.

![Virtual event format and platform fields](docs/images/event-format-location.png)

![Presentation review workflow](docs/images/presentation-review.png)

## Main workflows

### Portfolio and event progress

Track:

- Event name, modality, date, and delivery format
- **Virtual** events with platform or meeting details
- **In-person** events with venue, city, and country
- Expected attendees, audience, speakers, and owners
- Physician CVs, honorarium schedules, contracts, and agreement expiry dates
- Event-specific honorarium amount and approval status
- Presentation slide upload, review, requested changes, and approval
- **IRF** reference and approval status
- Cross-border review, budget, sponsors, objectives, topics, risks, and close-out

Readiness is calculated from configurable checkpoints, including:

1. Commercial brief
2. Medical or educational objective
3. Event date, format, and location or virtual platform
4. Audience and attendance estimate
5. Physician identification and vetting
6. Current physician CVs
7. Physician honorarium schedules and agreements
8. Event-specific honorarium or payment approval
9. Budget and sponsor documentation
10. IRF or funding approval
11. Cross-border review
12. Topics and materials
13. Presentation slides reviewed and approved
14. Execution readiness
15. Reconciliation and impact reporting

### Physician CV, honorarium, and agreement record

Open **Physicians & agreements** to maintain one reusable record per physician. Each record supports:

- Profile details, specialty, institution, role, country, and professional email
- One current CV in PDF, DOC, or DOCX format
- Manually entered honorarium service rows with service name, rate type, rate, currency, and notes
- A supporting honorarium rate-card file in PDF, Office, CSV, PNG, or JPG format
- An executed contract or agreement in PDF, DOC, or DOCX format
- Agreement type, reference, effective date, **agreement expiry date**, and notes
- Automatic statuses such as **Agreement missing**, **Contract file missing**, **Not yet effective**, **Expiring soon**, **Expired**, and **Active**
- Event-date checks that flag an agreement beginning after, or expiring before, the scheduled event
- Assignment of one physician record to multiple events
- Physician-register CSV export

The honorarium editor includes a **Load sample rate card** option containing 12 demonstration service rows. The same anonymized values are included in [`templates/sample-honorarium-example.csv`](templates/sample-honorarium-example.csv). Confirm all rates against the current signed agreement before use.

![Honorarium and agreement editor](docs/images/physician-honorarium-agreement.png)

### Event format and location

Every event is classified as either:

- **In-person** — venue, city, and country are captured and shown in the event register.
- **Virtual** — an approved platform or meeting detail can be entered instead of a physical location.

Changing the format updates the fields shown in the event drawer and affects the date/location readiness checkpoint.

### Presentation slides: review and approval

Each event can store one current presentation deck in PPT, PPTX, or PDF format, up to 30 MB. The event record includes:

- Presentation filename and version
- Review status
- Review owner
- Review due date
- Review comments or required changes
- Approved-by name
- Approval date

Available statuses are **Not uploaded**, **Draft**, **Submitted for review**, **In review**, **Changes requested**, **Approved**, and **Not required**.

An uploaded deck must be marked **Approved** before the presentation milestone is complete. Replacing an approved file resets it to **Draft** and clears the earlier approval. Upcoming events with an incomplete presentation review are surfaced in risk reporting.

### Event-specific honorarium

Each event drawer has an editable honorarium record for:

- Total amount
- Currency
- Approval or payment status
- Service, hours, travel compensation, payment owner, approval reference, and exception notes
- Physician service-rate references from the shared physician records

Updating the event honorarium also updates its progress checkpoint.

![Event honorarium record](docs/images/event-honorarium-drawer.png)

### Email-to-event intake

Paste an anonymized commercial-team email to detect:

- Event and modality
- Proposed date
- Virtual or in-person format
- Venue and physical location, or virtual platform
- Attendee estimate and audience
- Proposed physicians
- Honorarium and budget
- Sponsor support
- IRF reference and status
- Cross-border indicators
- Medical requests and due date
- Missing CV, rate schedule, agreement expiry, presentation-review owner, and approval information

The analyzer is local and rule-based. It does not connect to an inbox or send content to an external AI service.

### Medical review, budget, and reporting

The prototype includes Medical-review routing and modality-specific topic suggestions, presentation-review routing, budget and sponsorship views, governance exceptions, agreement-expiry reminders, event and physician CSV exports, and configurable workflow settings.

## File storage and privacy

This is a static prototype. Event and profile metadata is stored in browser `localStorage`. Uploaded CVs, rate cards, contracts, and presentation decks are stored as file blobs in browser IndexedDB.

Files therefore:

- Stay on the current computer and browser profile
- Are not committed to the GitHub repository
- Are not uploaded to GitHub Pages
- Are not automatically shared with colleagues
- Are removed when browser site data is cleared
- Must be uploaded again on another device or browser

Do not commit real physician CVs, contracts, rate cards, presentation decks, payment records, patient information, credentials, or confidential email exports to the repository. A production system needs authenticated, encrypted enterprise document storage, role-based access, retention controls, audit history, and country-specific governance rules. See [`docs/PRODUCTION_ARCHITECTURE.md`](docs/PRODUCTION_ARCHITECTURE.md).

## Run locally

No package installation or build step is required.

Open `index.html` directly in a modern browser, or serve the folder locally:

```bash
python3 -m http.server 8080
```

Then open `http://localhost:8080`.

Serving the site over HTTP or HTTPS is recommended because browser file-storage behavior can be more restrictive for a directly opened HTML file.

## Publish to GitHub Pages

The repository includes `.github/workflows/pages.yml`.

1. Create a GitHub repository.
2. Upload the **contents of this folder** so `index.html` is at the repository root.
3. Include the hidden `.github` folder and `.nojekyll` file.
4. Commit the files to the `main` branch.
5. Open **Settings → Pages** in the repository.
6. Select **GitHub Actions** as the source.
7. Open the **Actions** tab and wait for **Deploy static site to GitHub Pages** to finish.

Command-line upload:

```bash
git init
git add .
git commit -m "Add IO&E medical event hub"
git branch -M main
git remote add origin <YOUR_REPOSITORY_URL>
git push -u origin main
```

Detailed deployment instructions are in [`docs/DEPLOYMENT.md`](docs/DEPLOYMENT.md).

## Repository structure

```text
.
├── .github/workflows/pages.yml
├── docs/
│   ├── images/
│   ├── DEPLOYMENT.md
│   ├── PRODUCTION_ARCHITECTURE.md
│   └── USER_GUIDE.md
├── templates/
│   ├── sample-honorarium-example.csv
│   └── honorarium-rate-card-blank.csv
├── .gitignore
├── .nojekyll
├── CHANGELOG.md
├── README.md
├── SECURITY.md
├── index.html
└── robots.txt
```

## Demo reset

Use **Reset demo** in the application header to restore sample events and profiles. Resetting also deletes locally stored CVs, rate cards, contracts, and presentation decks for this prototype.

## Documentation

- [User guide](docs/USER_GUIDE.md)
- [GitHub Pages deployment](docs/DEPLOYMENT.md)
- [Production architecture considerations](docs/PRODUCTION_ARCHITECTURE.md)
- [Security and privacy guidance](SECURITY.md)
- [Changelog](CHANGELOG.md)
