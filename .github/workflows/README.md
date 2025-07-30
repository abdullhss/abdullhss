# GitHub Workflows

This directory contains GitHub Actions workflows that automatically update the repository.

## Workflows

### `update-readme-stats.yml`

This workflow automatically generates and updates GitHub statistics that are displayed in the main README.md file.

**Triggers:**
- Manual dispatch (workflow_dispatch)
- Daily at midnight UTC (cron: '0 0 * * *')

**What it does:**
1. Generates GitHub stats card showing:
   - Total stars, commits, pull requests, issues
   - Private repository contributions (if token provided)
   - Custom theme matching the README design
2. Generates top languages card showing:
   - Most used programming languages
   - Percentage breakdown
   - Compact layout
3. Commits the generated SVG files to the `stats/` directory
4. Pushes changes to the repository

**Required Secrets:**
- `GH_TOKEN`: GitHub Personal Access Token with repo permissions

**Output Files:**
- `stats/github-stats.svg` - Main statistics card
- `stats/top-langs.svg` - Top languages card

## Setup Instructions

1. **Create a GitHub Personal Access Token:**
   - Go to GitHub Settings → Developer settings → Personal access tokens
   - Generate a new token with `repo` permissions
   - Copy the token

2. **Add the token to repository secrets:**
   - Go to your repository Settings → Secrets and variables → Actions
   - Create a new secret named `GH_TOKEN`
   - Paste your personal access token

3. **Enable the workflow:**
   - The workflow will run automatically once set up
   - You can also trigger it manually from the Actions tab

## Customization

To customize the stats appearance, modify the workflow parameters in `.github/workflows/update-readme-stats.yml`:

- `theme`: Change the color theme (react, dark, light, etc.)
- `bg_color`: Background color (hex code)
- `title_color`: Title color (hex code)
- `text_color`: Text color (hex code)
- `hide_border`: Show/hide border
- `show_icons`: Show/hide icons

## Troubleshooting

**Workflow fails with permission errors:**
- Ensure the `GH_TOKEN` secret is properly set
- Check that the token has the necessary permissions

**Stats not updating:**
- Verify the workflow is running successfully
- Check that the `stats/` directory exists and is tracked by git
- Ensure the README.md references the correct file paths

**Authentication issues:**
- Regenerate the GitHub token if it expires
- Ensure the token has the correct scope (repo access) 