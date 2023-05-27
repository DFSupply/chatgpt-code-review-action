# OpenAI Code Review

A GitHub Action that uses OpenAI GPT3.5-turbo to analyze code in pull request comments.

## Usage

To use this action in your workflow, add the following step:

```yaml
name: OpenAI Code Review
uses: DFSupply/chatgpt-code-review-action@main
with:
    REVIEW_COMMENT_PREFIX: 'reviewbot:'
    FULL_REVIEW_COMMENT: 'reviewbot'
    OPENAI_TOKEN: ${{ secrets.OPENAI_API_KEY  }}
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN  }}
```

## Inputs

This action accepts the following inputs:

- `PROGRAMMING_LANGUAGE` (optional): The programming language of the code in the GitHub repository. If not provided, the detected programming language will be used.
- `OPENAI_TOKEN` (required): The API token for the OpenAI ChatGPT API.
- `GITHUB_TOKEN` (required): The API token for the Github API.
- `FULL_REVIEW_COMMENT` (required): The comment to trigger code review for the pull request.
- `REVIEW_COMMENT_PREFIX` (required): The comment prefix to trigger code review with the comment.
- `GITHUB_BASE_URL` (optional): The base URL for the GitHub API.
- `MAX_CODE_LENGTH` (optional): The maximum code length for the pull request code to be sent to OpenAI. The default value is 30000.
- `PROMPT_TEMPLATE` (optional): The template for the FULL_REVIEW_COMMENT prompt. The default value is:
```
Please analyze the pull request's code and inform me whether it requires optimization, and provide an explanation for your decision:

${code}
```
- `ANSWER_TEMPLATE` (optional): The template for the answer sent to the GitHub comment. The default value is:
```
Automated Code Review:

${answer}
```

## Github

### Code Review for a specific file

If a comment starts with `reviewbot:`, you can use it to communicate with ChatGPT just like you would in the official interface.

To reference the diff code of the pull request in your comment, use ${code}:

```
reviewbot: Please explain the usage of the `getPrCode` function:

${code}
```

To reference the diff code of a specific file in the pull request, use ${file:filename}:

```
reviewbot: Can you check if there are any bugs in the following code?

${file:dist/index.js}
```

## License

The code in this repository is licensed under the MIT license. See `LICENSE` for more information.
