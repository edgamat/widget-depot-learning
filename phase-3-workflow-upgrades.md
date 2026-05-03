# Phase 3 Workflow Upgrades

I am learning how to use Claude Code to improve my overall productivity when developing software.
There are a few areas of friction that I want to improve upon.

1. Generating better stories
2. Generate Milestones/Stories in GitHub
3. More predictable creation of issues in GitHub
4. Have the agent respond (locally) to PR feedback
5. Add integration tests (e.g. Playwright)

**NOTE** In this context, an agent is any AI assistant a human uses to delegate tasks to. For 
example, I am currently using Claude Code as my agent.

## Current Workflow

My requirements gathering workflow is to take a set of requirements (`requirements.md`) and create a
document that defines the goals, scope, and constraints of the work (`prd.md`). I then add a list
of milestones to the `prd.md` that provide review points in the process to verify the work is still
on target and make any adjustments. Both documents live in the repo as markdown files:

```
/docs/requirements.md
/docs/prd.md
```

**NOTE** I used to record these details in OneNote. But I find that including them in the source code repo
makes them easier to share and manage.

For each milestone, I ask an agent to breakdown all requirements into user stories and store theme
in the code repo:

```
/docs/milestone-01/01-first-user-story.md
/docs/milestone-01/02-second-user-story.md
...
/docs/milestone-02/01-first-user-story.md
/docs/milestone-02/02-second-user-story.md
...
```

I refine the stories one milestone at a time. Once I have completed a milestone, I start refining
the stories for the next milestone. I do this to ensure I can take what I have learned from one
milestone and incorporate that feedback into the next milestone.

I have an agent generate user stories with my guidance. When a user story is ready, I ask the
agent to add issues to GitHub to implement the story. It always creates a single issue per story. I
use the issues as 'tasks' for the agent to execute ('Let's work on issue #12').

## 1. Generating Better Stories

I have noticed that I do not have a structured approach for coming to a shared understanding with 
an AI agent for what should be written into stories. I let the agent create each story, I manually
review them, and make any changes I feel are necessary (either manually or by using an agent).

I'd like the get the agent to 'grill me' during this process a bit more than it does now. The goal
is to find gaps in the requirements and to have a more complete representation of what is required
and how to verify it is working (acceptance criteria).

I want to guard against the agent going overboard and creating huge stories. I want to give the
agent guidance on how to define stories (progressive discovery of user story standards). For
example, have a markdown file an agent can reference that contains instructions on how 
to write good user stories.

I'd like to have a skill that I can use to codify the rules on how to refine a milestone into user
stories:

Skill: `/refine-milestone {{Milestone #}}`

For example, I would use the `/refine-milestone` skill to add one or more stories for the goals of
the milestone I am working on:

`/refine-milestone 2`

When the `/refine-milestone` skill is run, I want the agent to present me with a plan for creating
user stories. Once the plan is confirmed, I want the agent to create draft versions of the stories
in the repo for me to review. I expect there to be back and forth, questions asked, ideas clarified,
and so on. But eventually, the agent and I will agree that the stories are ready to be shared with
the rest of the development team.

## 2. Generate Milestones/Stories in GitHub

I want to still use the repo as a starting point for the stories, but I want to ultimately have the
milestone, the user stories, and the associated tasks stored in GitHub as issues. The markdown files
in the repo are more of a 'scratchpad' where I can collaborate and brainstorm ideas. Once I am
ready to share the stories with the rest of my team, I create the issues in GitHub. I use an agent
to copy the stories to GitHub issues.

Here is what I would prefer the new workflow to be like:

After the `/refine-milestone` skill is run, I want to run a new skill to share the details with
the rest of the team using GitHub issues:

Skill: `/share-milestone {{Milestone #}}`

When called, this skill should perform the following:

- create an issue in GitHub for each user story. The contents of the repo markdown file for the
  story are cloned to the issue.
- create an issue in GitHub for the milestone. Link each user story issue to the milestone story as
a sub issue.

## 3. More predictable creation of issues in GitHub

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

## 4. Have the agent respond (locally) to PR feedback

Currently, my workflow is to have the agent create a pull request for me to review. I review the PR
and then apply the feedback in the code. Once the feedback is incorporated, a new commit is pushed
to the PR branch. What I would like to do is add feedback to the PR (in GitHub). Then ask the agent
to read the comments from the PR, apply the changes, and then push a new commit addressing the
feedback. It should prompt me with any questions it has to ensure it understands the feedback
correctly.

Skill: `/address-pr {{PR #}}`

## 5. Add integration tests (e.g. Playwright)

I like having more than unit tests to verify the correctness of a solution, and to help discover
regressions to existing behavior. I'd like to add an integration test project to the solution and
have it run Playwright tests against the local copy of the application. Once established, my goal
would be to instruct the agent to add appropriate integration tests for each story.

**NOTE** Needs lots of help writing these tests. Where to find the data, how to verify the results,
sample files, inputs, etc.
