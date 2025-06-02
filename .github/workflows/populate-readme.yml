from dotenv import dotenv_values
from pathlib import Path

# Load config from .project
config = dotenv_values(".project")

# Fallback defaults
defaults = {
    "PROJECT_NAME": "Untitled Research Project",
    "PROJECT_DESCRIPTION": "No description provided.",
    "PI_NAME": "Firstname Lastname",
    "PI_AFFILIATION": "Newcastle University",
    "RSE_NAME": "Firstname Lastname",
    "RSE_AFFILIATION": "Newcastle University",
    "LICENSE": "TBD",
    "FUNDING_BODY": "UK Research Councils",
    "GRANT_REF": "EP/XXXXXX/1",
    "FUNDING_TITLE": "Please update the project title",
    "DEPLOYMENT_TARGET": "To be defined",
    "BUILT_WITH": "",
    "REPO_URL": "https://github.com/example/project",
    "WEBSITE_URL": "",
    "START_DATE": "TBD",
    "END_DATE": "TBD",
}

def get(key):
    return config.get(key, defaults.get(key, f"Unknown {key}"))

readme_path = Path("README.md")
readme_text = readme_path.read_text()

# Replace basic placeholders
for key in defaults:
    readme_text = readme_text.replace(f"{{{{{key}}}}}", get(key))

# Format 'Built With'
def format_built_with(entry):
    if "|" in entry:
        name, url = entry.split("|")
        return f"- [{name.strip()}]({url.strip()})"
    return f"- {entry.strip()}"

built_with = get("BUILT_WITH")
if built_with.strip():
    built_with_md = "\n".join(
        format_built_with(entry) for entry in built_with.split(",") if entry.strip()
    )
else:
    built_with_md = "_This project has no listed dependencies yet._"

readme_text = readme_text.replace("{{BUILT_WITH_MD}}", built_with_md)

# Team table
team_md = f"""
| Name              | Role | Affiliation          |
|-------------------|------|----------------------|
| {get('PI_NAME')} | PI   | {get('PI_AFFILIATION')} |
| {get('RSE_NAME')} | RSE  | {get('RSE_AFFILIATION')} |
""".strip()
readme_text = readme_text.replace("{{TEAM_MD}}", team_md)

# Acknowledgements
ack_md = (
    f"This work was funded by a grant from the {get('FUNDING_BODY')} "
    f"({get('GRANT_REF')}), “{get('FUNDING_TITLE')}”."
)
readme_text = readme_text.replace("{{ACKNOWLEDGEMENTS}}", ack_md)

readme_path.write_text(readme_text)
print("[+] README.md successfully populated.")

