# upload-artifact
This GitHub Action, named "Upload artifact," is an enhanced wrapper around GitHub's official upload-artifact - version 3.0 action. It includes an additional step for archiving files before uploading them as an artifact.

# Inputs

| Input              | Description                                                                                              | Required | Default |
|--------------------|----------------------------------------------------------------------------------------------------------|----------|---------|
| `name`             | The name for the artifact.                                                                               | Yes      | -       |
| `path`             | A file, directory, or wildcard pattern that describes what to upload.                                    | Yes      | -       |
| `if-no-files-found`| Behavior if no files are found using the provided path. Options: `warn`, `error`, `ignore`.              | No       | `warn`  |
| `retention-days`   | Duration after which artifact will expire in days (0 for default). Min 1 day, max 90 days.               | No       | `0`     |
| `working-directory`| Optional working directory to start the `path` search from.                                               | No       | `./`    |

# Action Workflow

**Archive Artifacts:**

- It archives the specified files (based on the path input) into a .tar file.
- If no files are found, it handles the situation based on the if-no-files-found input.

**Upload Artifacts:**

- This step is conditional and executes only if the archival process is successful.
- It uses GitHub's upload-artifact@v3 to upload the created .tar archive.

**Remove Archive:**

- After uploading, it removes the temporary **.tar** file created during the archival step.

# Usage

To use this action in your workflow, include it as a step in your **.yml** workflow file with necessary inputs. Ensure to provide values for required inputs **name** and **path**.
```yaml
steps:
- uses: echapmanFromBunnings/upload-artifact@3.0
  with:
    name: 'artifact-name'
    path: 'path/to/your/files/**/*'
    if-no-files-found: 'warn' # Optional
    retention-days: 10 # Optional
    working-directory: './path/to/start' # Optional
```
