# AI Time Tracking Workflow Template

This GitHub Actions workflow template automatically logs development time to Teamwork when pull requests labeled with "AI" are merged. It estimates the time that would have been required for a senior developer to complete the task based on the scope of code changes.

## Features

- 🤖 **Automatic Time Estimation**: Analyzes code changes to estimate development time
- 🏷️ **Label-Based Triggering**: Only runs when PRs have the "AI" label
- ⏱️ **Teamwork Integration**: Automatically creates time entries in Teamwork
- 📊 **Smart Analysis**: Considers lines added, deleted, and files changed
- 💬 **PR Comments**: Adds status comments to the pull request

## Setup

### Required Secrets

You need to configure the following secrets in your repository or organization:

#### Enterprise-wide Secrets (Organization Level)
- `TEAMWORK_API_TOKEN`: Your Teamwork API authentication token
- `TEAMWORK_SITE_URL`: Your Teamwork site URL (e.g., `https://yourcompany.teamwork.com`)

#### Repository-specific Secrets
- `TEAMWORK_PROJECT_ID`: The ID of the Teamwork project to log time to

### Getting Teamwork API Credentials

1. **API Token**: Go to your Teamwork account settings → API & Mobile Apps → Generate API Key
2. **Site URL**: This is your Teamwork subdomain URL
3. **Project ID**: Find this in the URL when viewing a project in Teamwork, or use the Teamwork API to list projects

### How to Use

1. **Add the Workflow**: Copy the `ai-time-tracker.yml` file to your repository's `.github/workflows/` directory
2. **Configure Secrets**: Set up the required secrets in your repository/organization settings
3. **Label PRs**: Add the "AI" label to pull requests that involve AI-assisted development
4. **Merge PRs**: When labeled PRs are merged, time will be automatically logged

## Time Estimation Logic

The workflow uses a basic algorithm that can be enhanced with AI:

- **Base Time**: 15 minutes per file changed
- **Line-based Time**: 1 minute per 10 lines added
- **Refactoring Time**: 1 minute per 20 lines deleted
- **Bounds**: Minimum 30 minutes, maximum 8 hours

## Customization

You can customize the time estimation logic by modifying the calculation in the "Estimate development time" step. For more sophisticated estimates, you could integrate with AI services like GitHub Copilot API or OpenAI.

## Troubleshooting

### Common Issues

1. **Missing Secrets**: Ensure all required secrets are configured
2. **Invalid Project ID**: Verify the Teamwork project ID is correct
3. **API Authentication**: Check that the API token has the necessary permissions
4. **Label Not Found**: Ensure the "AI" label exists in your repository

### Debugging

Check the workflow logs for detailed information about:
- Code change analysis
- Time estimation calculations
- API calls to Teamwork
- Error messages

## API Reference

This workflow uses the Teamwork Time Tracking API:
- **Endpoint**: `POST /projects/api/v3/projects/{project-id}/time.json`
- **Documentation**: https://apidocs.teamwork.com/docs/teamwork/v3/time-tracking/post-projects-api-v3-projects-project-id-time-json

## License

This workflow template is provided as-is for use within your organization.