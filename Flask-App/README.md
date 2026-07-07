# E-CarStart — Flask + Tableau EV Analytics Site

A small Flask web app that embeds your **Electric Car Analytics Dashboard**
(Tableau Public) directly into a custom-built site.

## Run it locally

```bash
cd e-carstart
python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate
pip install -r requirements.txt
python app.py
```

Then open **http://127.0.0.1:5000** in your browser.

## Project structure

```
e-carstart/
├── app.py                  # Flask routes + Tableau embed URL
├── requirements.txt
├── templates/
│   ├── base.html           # nav, footer, shared layout
│   └── index.html          # all page sections
└── static/
    ├── css/style.css
    └── js/script.js
```

## Swapping in your own Tableau viz

**Dashboard section** uses a simple iframe pointed at the viz name/sheet
in `app.py`:

```python
TABLEAU_VIZ = "ElectricCarAnalyticsDashboard_17832499846150"
TABLEAU_SHEET = "Dashboard1"
```

**Story section** uses Tableau's own embed snippet (copy-pasted from the
"Share" button on your Tableau Public viz), pasted directly into
`templates/index.html`. If you republish the story, grab the new embed
code from Tableau Public and swap the `<div class='tableauPlaceholder'>…`
block in the Story section, and update the `id` you reference in
`static/js/script.js` (`viz1783352246254`) to match.

You can find the viz name and sheet name in your Tableau Public URL:
`public.tableau.com/app/profile/<profile>/viz/<VIZ_NAME>/<SHEET_NAME>`

## Deploying so others can see it

Tableau Public embeds work from any publicly reachable URL. Easiest free
options for a student project:
- **Render** or **Railway** (free tier, deploys straight from GitHub)
- **PythonAnywhere** (simple Flask hosting, good for portfolio links)

Push this folder to a GitHub repo first, then connect it to whichever
host you choose — both support "deploy from GitHub" with almost no config
for a small Flask app like this.

## Customizing

- Colors, fonts: `static/css/style.css` (`:root` variables at the top)
- Copy: `templates/index.html`
- Team section: currently a single "Built by" card — add more `.team-card`
  blocks if you collaborate with others.
- Contact form: currently just flashes a confirmation message. Wire it to
  an email service (Flask-Mail, SendGrid, etc.) if you want real delivery.
