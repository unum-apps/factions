The Link Question Topic Pipeline
================================

This takes in a link and generates Questions, generates new Topics if needed, and Tags the Questions with the Topics.

Steps:
- Submit Link
- Generate Questions
- Verify Questions
- Generate Topics
- Verify Topics
- Generate Tags
- Verify Tags
- Verify Link

# Submit Link

This creates a submitted link.

Get a link and use the following below into ChatGPT using this prompt:

## Prompt

Give this link, generate a unique slug, dashes no underscores, based on the link with name at front up to 48 chars, and end with the date with a suffix of .yaml. Only ASCII

```yaml
link:
slug: (based on the link with name at front up to 48 chars, no date)
file: (full filename with date at end and yaml suffix)
```

## Branch

Checkout this repo and create a branch of your username/slug from above.

## File

Create a file in `lqt/submitted` named as above with the generated content. Do a commit.

# Generate Questions

Paste the file contents into ChatGPT using this prompt:

## Prompt

Please generate 10 multiple choice questions and add to the link YAML in this format, only ASCII:

```yaml
questions:
- question: (put the question here)
  correct: (put the correct answer here)
  incorrect:
  - (put each)
  - (incorrect anwser)
  - (here)
```

Link:
```yaml
(put lqt/submitted file here)
```

## File

Create a file in `lqt/questions` named as above with the generated content. Do a commit.

# Verify Questions

Go into the file and verify accuracy. Edit and get rid of questions that don't make sense.

## File

Add this block:

```yaml
verified:
  questions: (your github username here)
```

Save and do a commit

# Generate Topics

This creates the Topics for the quiz.

## Prompt

Given this list of questions from a link, and the following existing topics, please first suggest any new topics in the questions not covered in the existing list in the same YAML format as the topics provided. The tag of a topic should be short and knowable, a capitalized acronym if it exists, etc. Only ASCII. Add link, slug, and file, as well to the top.

Questions
```yaml
(put lqt/questions file here)
```

Topics

```yaml
(put lqt/topics.yaml here)
```

## File

Create a file in `lqt/topics` named as above with the generated content. Do a commit.

# Verify Topics

Go into the file and verify accuracy. Edit and get rid of topics that don't make sense or are too narrow.

## File

Go into in `lqt/topics.yaml` and add only the topics we want to make permanent.

Save both files and do a commit.

# Generate Tags

This associate Topics with Questions.

## Prompt

Given this list of questions from a link, and the following topics, please add tags to the questions YAML:

Tags in new YAML (lease existing fields alone)
```yaml
questions:
- question: (put the question here)
  correct: (put the correct answer here)
  incorrect:
  - (put each)
  - (incorrect anwser)
  - (here)
  tags:
  - (Topic tag)
  - (Topic tag)
```

Questions
```yaml
(put lqt/questions file YAML here)
```

Topics
```yaml
(put lqt/topics.yaml here)
```

## File

Create a file in `lqt/tags` named as above with the generated content. Do a commit.

# Verify Tags

Go into the file and verify accuracy. Edit and get rid of tags that don't make sense.

Add to the verify block:

```yaml
verified:
  tags: (your github username here)
```

Commit.

# Verify Link

## File

Copy file from `lqt/tags` to `lqt/verified/`. Commit.

## Pull Request

Push and create a PR named `LGT: (link)`. Send to the other approvers to merge.

Note: You may have to rebase when Topic changes overlap.
