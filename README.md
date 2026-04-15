AI Content Generator (n8n + MkDocs)

An automated content generation system that creates product marketing copy using n8n workflows and publishes it as a live documentation site using MkDocs.



Overview

This project demonstrates how to build an end-to-end automation pipeline:

Accept a product name via webhook
Generate multiple versions of marketing copy
Convert content into Markdown
Save files automatically to disk
Render content as a live website



Tech Stack

n8n – Workflow automation
Node.js – Runtime environment
MkDocs – Static site generator
Markdown – Content format


Features

Webhook-triggered content generation
3 variations of product copy:

Professional
Casual
Persuasive
Automatic Markdown file creation
Dynamic file naming (slug-based)
Live preview via MkDocs
File system integration



Project Structure


ai-content-generator/
├── n8n/
│   └── n8n-workflow.json
├── site/
│   ├── docs/
│   │   ├── index.md
│   │   └── *.md
│   └── mkdocs.yml
├── .gitignore
└── README.md




Getting Started

1. Clone the Repository


git clone https://github.com/yourusername/ai-content-generator.git
cd ai-content-generator




2. Start n8n


N8N_BLOCK_FILE_ACCESS_TO_N8N_FILES=false \
N8N_RESTRICT_FILE_ACCESS_TO= \
n8n start




3. Import Workflow

1. Open n8n in browser
2. Click **Import Workflow**
3. Select:


n8n/n8n-workflow.json




4. Run MkDocs


cd site
mkdocs serve


Open:


http://127.0.0.1:8000




5. Trigger Content Generation


curl -X POST http://localhost:5678/webhook/generate-content \
-H "Content-Type: application/json" \
-d '{"product": "Smart Fitness Watch"}'




Example Output

A request like:


Smart Fitness Watch


Generates:


site/docs/smart-fitness-watch.md

With content:

* Professional copy
* Casual copy
* Persuasive copy
* Timestamp



Key Implementation Details

* Markdown is generated dynamically in n8n Code nodes
* Binary conversion handled manually using Base64 encoding
* Files written using n8n Read/Write File node
* macOS file restrictions resolved via environment configuration


Known Issues & Fixes

| Issue                  | Solution                            |
| ---------------------- | ----------------------------------- |
| Webhook not registered | Publish workflow                    |
| No output data         | Trigger workflow correctly          |
| Binary file missing    | Use Code node for Base64 conversion |
| File not writable      | Disable n8n file restrictions       |
| Path errors            | Use absolute paths + correct casing |



Security Note

The current setup disables file system restrictions:


N8N_RESTRICT_FILE_ACCESS_TO=


️ This is safe for local development only.
For production, restrict access to a specific directory.

---

Future Improvements

Add frontend UI for input (replace curl)
Integrate real AI APIs
Auto-update MkDocs navigation
Add image generation
Deploy site (Netlify / GitHub Pages)


Learning Outcomes

This project covers:

Workflow automation with n8n
API/webhook integration
File system operations
Static site generation
Debugging real-world system issues



Author

Built as a hands-on automation and content generation project.



️Support

If you find this useful, consider starring the repository.

