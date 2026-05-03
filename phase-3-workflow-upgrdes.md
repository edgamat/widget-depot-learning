# Phase 3 Workflow Upgrades

There are a few areas of friction that I want to improve upon.

1. Generate Milestones/Stories in GitHub
2. Generating better stories
2. More predictable creation of issues in GitHub
3. Have the agent respond (locally) to PR feedback
4. Add integration tests (e.g. Playwright)

## Current Workflow

My requirements gathering workflow is to take a set of requirements (`requirements.md`) and create a
document that defines the goals, scope, and constraints of the work (`prd.md`). I then add a list
of milestones to the `prd.md` that provide review points in the process to verify the work is still
on target and make any adjustments. Both documents live in the repo as markdown files:

```
/docs/requirements.md
/docs/prd.md
```

For each milestone, I breakdown all the requirements into user stories and store these in the code
repo:

```
/docs/milestone-01/01-first-user-story.md
/docs/milestone-01/02-second-user-story.md
...
/docs/milestone-02/01-first-user-story.md
/docs/milestone-02/02-second-user-story.md
...
```

I have the agent generate these user stories with my guidance. When the story is ready, I ask the
agent to add issues to GitHub to implement the story. It always creates a single issue per story. I
use the issues as 'tasks' for the agent to execute ('Let's work on issue #12').

## Generate Milestones/Stories in GitHub

I want to still use the repo as a starting point for the stories, but I want to ultimately have the
milestone, the user story and the associated tasks stored in GitHub as issues.

## Generating Better Stories

I have noticed that I do not have a structured approach for coming to a shared understanding of what
should be written into stories. I let the agent create each story, I manually review them, and make
any changes I feel are necessary (either manually or by using an agent).

I'd like the get the agent to 'grill me' during this process a bit more than it does now. The goal
is to find gaps in the requirements and to have a more complete representation of what is required
and how to verify it is working (acceptance criteria).

I want to guard against the agent going overboard and creating huge stories. I want to give the
agent grilling me guidance on how to define stories (progressive discovery of user story standards).

I'd like to have a skill that I can use to codify the rules on how to add a new story to the
backlog.

I'd like to have the agent read 'user story standards' from a markdown file containing
instructions for how it should write the user stories.

Skill: `/refine-milestone {{Milestone #}}`

For example, I would use the `/refine-milestone` skill to add one or more stories for one of the goals of
the milestone I am working on:

`/refine-milestone 2`

## More predictable creation of issues in GitHub

I have found that when asking the agent to create issues in GitHub for a user story, 'drift' is
introduced. The issues in GitHub miss some of the details of the user story or new requirements
are added. I want to instruct the agent to be more mindful of this undesirable outcome. But I also
want the agent to split a story into multiple issues when appropriate. I wouldn't expect a human
to always create a single PR for each story. I would like to provide instructions to the agent to
create separate issues in GitHub when there are good reasons to have more than one PR per user
story. 

For example, I would prefer that changes to the data model (requiring a database migration) be
made using a separate PR from the code changes dependent upon that change. In my experience, the
data model changes are where there is a higher chance of mis-communication or missed expectations
by humans and agents alike. It makes sense to me to have a separate PR for such changes to ensure
we are on the same page before building on those changes.

I also feel that the backend API work and the frontend UI work should sometimes (not always) be 
performed in separate PRs. A simple vertical slice of functionality can represent dozens of files
and hundreds of lines of code. The code review process is a bottleneck on this project and making
smaller PRs for review can make the review process more efficient. But as with most things, it is a
balance between too many PRs and too marge PRs. I would want to give the agent explicit instructions
when asking it to create the GitHub issues on how to break the story into issues (tasks).

I'd like to have a skill that I can use to codify the rules on how to refine a story into one or
more GitHub issues.

Skill: `/refine-story {{Milestone #}} {{Story #}}`

**NOTE** Give the skill examples of situations when to keep a story as a single issue or when to 
split it into separate issues.

## Have the agent respond (locally) to PR feedback

Currently, my workflow is to have the agent create a pull request for me to review. I review the PR
and then apply the feedback in the code. Once the feedback is incorporated, a new commit is pushed
to the PR branch. What I would like to do is add feedback to the PR (in GitHub). Then ask the agent
to read the comments from the PR, apply the changes, and then push a new commit addressing the
feedback. It should prompt me with any questions it has to ensure it understands the feedback
correctly. Perhaps a skill? `/respond-to-pr-feedback {{PR #}}`?

## Add integration tests (e.g. Playwright)

I like having more than unit tests to verify the correctness of a solution, and to help discover
regressions to existing behavior. I'd like to add an integration test project to the solution and
have it run Playwright tests against the local copy of the application. Once established, my goal
would be to instruct the agent to add appropriate integration tests for each story.

**NOTE** Needs lots of help writing these tests. Where to find the data, how to verify the results,
sample files, inputs, etc.
