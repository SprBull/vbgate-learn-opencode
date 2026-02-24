---
title: "5.15 GitLab Integration"
subtitle: "Using OpenCode in GitLab CI/CD"
course: "OpenCode Practical Course"
stage: "Stage 5"
lesson: "5.15"
duration: "15 minutes"
practice: "20 minutes"
level: "Advanced"
description: "Use OpenCode in GitLab Runner through GitLab CI/CD pipelines or GitLab Duo integration."
tags:
  - GitLab
  - CI/CD
  - Automation
prerequisite:
  - "5.14 GitHub Integration"
---

# GitLab Integration

OpenCode integrates into GitLab workflows through GitLab CI/CD pipelines or GitLab Duo integration. In both cases, OpenCode runs on your GitLab Runner.

## 📝 Lesson Notes

Key takeaways from this lesson:

<img src="/images/5-advanced/gitlab-notes.mini.jpeg"
     alt="GitLab Integration Notes"
     data-zoom-src="/images/5-advanced/gitlab-notes.jpeg" />

## Differences from GitHub Integration

Before diving into configuration, it's important to understand the differences between GitLab and GitHub integration:

| Feature | GitHub Integration | GitLab Integration |
|---------|-------------------|-------------------|
| Installation | Official command `opencode github install` | Manual config or community components |
| Official Support | OpenCode official GitHub App | Community-maintained CI components |
| Trigger | `/opencode` or `/oc` | `@opencode` (configurable) |
| Action/Component | `anomalyco/opencode/github@latest` | `nagyv/gitlab-opencode@2` |

::: tip Recommendation
If you use both GitHub and GitLab, GitHub integration is more "out-of-the-box". GitLab integration requires more manual configuration but offers greater flexibility. See [5.14 GitHub Integration](./14-github) for GitHub setup instructions.
:::

---

## GitLab CI

<AdInArticle />

OpenCode works in regular GitLab pipelines. It can be incorporated into pipelines as a [CI component](https://docs.gitlab.com/ee/ci/components/).

Here we use the community-created CI/CD component: [nagyv/gitlab-opencode](https://gitlab.com/nagyv/gitlab-opencode).

### Features

- **Custom Configuration**: Each job can enable or disable features using custom configuration directories (e.g., `./config/#custom-directory`)
- **Minimal Setup**: The CI component sets up OpenCode in the background, you only need to create configuration and initial prompts
- **Flexible**: The CI component supports various input parameters to customize behavior

### Setup

**1. Store Authentication**

Store the OpenCode authentication JSON as a **File type** CI environment variable:

- Go to **Settings** > **CI/CD** > **Variables**
- Add a variable, select **File** as the type
- Make sure to check **Masked and hidden**

Authentication JSON examples (choose based on your model provider):

```jsonc
// Anthropic
{
  "anthropic": {
    "type": "api",
    "key": "sk-ant-api03-xxx..."
  }
}

// OpenAI
{
  "openai": {
    "type": "api",
    "key": "sk-xxx..."
  }
}

// Multiple providers
{
  "anthropic": {
    "type": "api",
    "key": "sk-ant-api03-xxx..."
  },
  "openai": {
    "type": "api",
    "key": "sk-xxx..."
  }
}
```

**2. Configure .gitlab-ci.yml**

Add the following to `.gitlab-ci.yml`:

```yaml
include:
  - component: $CI_SERVER_FQDN/nagyv/gitlab-opencode/opencode@2
    inputs:
      config_dir: ${CI_PROJECT_DIR}/opencode-config
      auth_json: $OPENCODE_AUTH_JSON  # Variable name created in previous step
      command: optional-custom-command
      message: "Your prompt here"
```

::: tip Component Version
`@2` is the current major version. Check the [Component Catalog](https://gitlab.com/explore/catalog/nagyv/gitlab-opencode) for the latest version and complete list of input parameters.
:::

---

## GitLab Duo

OpenCode integrates into GitLab workflows. Mention `@opencode` in comments, and OpenCode will execute tasks in GitLab CI pipelines.

### Features

- **Triage Issues**: Let OpenCode review Issues and explain them
- **Fix and Implement**: Let OpenCode fix Issues or implement features, it will create new branches and submit Merge Requests
- **Secure**: OpenCode runs on your GitLab Runner

### Setup

OpenCode runs in GitLab CI/CD pipelines. Setup steps:

::: tip Official Documentation
Check the [GitLab Official Documentation](https://docs.gitlab.com/user/duo_agent_platform/agent_assistant/) for the latest instructions.
:::

1. Configure GitLab environment
2. Setup CI/CD
3. Get AI model provider API keys
4. Create service account
5. Configure CI/CD variables
6. Create flow configuration file

### glab CLI

The flow configuration uses [glab](https://gitlab.com/gitlab-org/cli)—GitLab's official command-line tool. It provides the ability to interact with GitLab API, including:

- List/create/manage Issues
- Operate Merge Requests
- View CI/CD status

OpenCode reads GitLab data and performs operations through glab.

<details>
<summary>Flow Configuration Example</summary>

```yaml
image: node:22-slim
commands:
  - echo "Installing opencode"
  - npm install --global opencode-ai
  - echo "Installing glab"
  - export GITLAB_TOKEN=$GITLAB_TOKEN_OPENCODE
  - apt-get update --quiet && apt-get install --yes curl wget gpg git && rm --recursive --force /var/lib/apt/lists/*
  - curl --silent --show-error --location "https://raw.githubusercontent.com/upciti/wakemeops/main/assets/install_repository" | bash
  - apt-get install --yes glab
  - echo "Configuring glab"
  - echo $GITLAB_HOST
  - echo "Creating OpenCode auth configuration"
  - mkdir --parents ~/.local/share/opencode
  - |
    cat > ~/.local/share/opencode/auth.json << EOF
    {
      "anthropic": {
        "type": "api",
        "key": "$ANTHROPIC_API_KEY"
      }
    }
    EOF
  - echo "Configuring git"
  - git config --global user.email "opencode@gitlab.com"
  - git config --global user.name "OpenCode"
  - echo "Testing glab"
  - glab issue list
  - echo "Running OpenCode"
  - |
    opencode run "
    You are an AI assistant helping with GitLab operations.

    Context: $AI_FLOW_CONTEXT
    Task: $AI_FLOW_INPUT
    Event: $AI_FLOW_EVENT

    Please execute the requested task using the available GitLab tools.
    Be thorough in your analysis and provide clear explanations.

    <important>
    Please use the glab CLI to access data from GitLab. The glab CLI has already been authenticated. You can run the corresponding commands.

    If you are asked to summarize an MR or issue or asked to provide more information then please post back a note to the MR/Issue so that the user can see it.
    You don't need to commit or push up changes, those will be done automatically based on the file changes you make.
    </important>
    "
  - git checkout --branch $CI_WORKLOAD_REF origin/$CI_WORKLOAD_REF
  - echo "Checking for git changes and pushing if any exist"
  - |
    if ! git diff --quiet || ! git diff --cached --quiet || [ --not --zero "$(git ls-files --others --exclude-standard)" ]; then
      echo "Git changes detected, adding and pushing..."
      git add .
      if git diff --cached --quiet; then
        echo "No staged changes to commit"
      else
        echo "Committing changes to branch: $CI_WORKLOAD_REF"
        git commit --message "OpenCode changes"
        echo "Pushing changes up to $CI_WORKLOAD_REF"
        git push https://gitlab-ci-token:$GITLAB_TOKEN@$GITLAB_HOST/$CI_PROJECT_PATH.git $CI_WORKLOAD_REF
        echo "Changes successfully pushed"
      fi
    else
      echo "No git changes detected, skipping push"
    fi
variables:
  - ANTHROPIC_API_KEY
  - GITLAB_TOKEN_OPENCODE
  - GITLAB_HOST
```

</details>

::: info Configuration Notes
- `$AI_FLOW_CONTEXT`, `$AI_FLOW_INPUT`, `$AI_FLOW_EVENT` are environment variables injected by GitLab Duo
- `$CI_PROJECT_PATH` is a GitLab predefined variable representing `<namespace>/<project>`
- For more GitLab predefined variables, refer to [GitLab CI/CD Variables Documentation](https://docs.gitlab.com/ee/ci/variables/predefined_variables.html)
:::

For detailed instructions, refer to [GitLab CLI agents documentation](https://docs.gitlab.com/user/duo_agent_platform/agent_assistant/).

---

## Usage Examples

::: tip Custom Trigger
You can configure a different trigger word instead of `@opencode`.
:::

### Explain Issue

Add a comment in a GitLab Issue:

```
@opencode explain this issue
```

OpenCode will read the Issue and reply with an explanation.

### Fix Issue

In a GitLab Issue:

```
@opencode fix this
```

OpenCode will create a new branch, implement changes, and open a Merge Request.

### Review Merge Request

Leave a comment in a GitLab Merge Request:

```
@opencode review this merge request
```

OpenCode will review the Merge Request and provide feedback.

---

## Common Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| CI component not found | Private GitLab instance may not access components on gitlab.com | Fork the component to your GitLab instance, or download and reference locally |
| `OPENCODE_AUTH_JSON` invalid | Wrong variable type (should be File not Variable) | Delete and recreate in CI/CD Variables, ensure **File** type is selected |
| glab authentication failed | `GITLAB_TOKEN` insufficient permissions | Ensure Token has `api`, `read_repository`, `write_repository` permissions |
| git push rejected | Branch protection rules | Configure in Settings > Repository > Protected Branches to allow bot pushes |
| OpenCode unresponsive | Runner network issues or invalid API key | Check Runner logs, verify API key is correct |

---

## Related Sections

- [5.14 GitHub Integration](./14-github) - GitHub Actions integration
- [5.1a Configuration Basics](./01a-config-basics) - Understanding OpenCode configuration file format
