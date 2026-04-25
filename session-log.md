## 2026-04-25 - Matt Edgar - Phase 3

**Working on** Milestone 2 - Story 1 (New Order)
**Duration:** 1.50 hours

**What happened:**
I changed my workflow. I created one issue in gitHub for the entire story, rather than separate issues for tasks. It did okay, but the PR it created was rather large (20 files, 900+ lines of code). I think it would be better for me to have CC break the story into 2 tasks, one for the backend (API changes) and one for the frontend (UI) changes.

I noticed after the PR was created that there was a business rule embedded in the developer notes of the story. This rule was not one I wanted and it was part of 3 stories. I have CC rework the stories (I asked it to change the existing stories or create a new one, and it opted for changing the existing stories). At the end of the plan, it gave me a list of steps to apply the changes to the existing PR.

The steps CC gave me were incomplete, it didn't give the proper steps to revert the EF Core migration, fix the data model and regenerate a new migration. It made a horrible mess of things. I ended up having to drop the docker volume and start the database over. I need to come up with a way for it to know what it should do when reversing an EF core migration.

**What worked well:**
Having CC do all the work in a single PR was okay. It consumed fewer tokens, but not a lot fewer.

**Questions or ideas:**
I need to pay more attention to the stories CC generates. That business rule in the developers nots should have been caught earlier.


Consumed 58% of available tokens (5 hour window)


## 2026-04-21 - Matt Edgar - End of Phase 2

**Working on** New Stories for Milestone 2
**Duration:** 1.50 hours

**What happened:**

I had CC breakdown Milestone 2 into stories. In Milestone 1 I had CC only provide the title and description of each story. The scope, notes and acceptance criteria were added on-demand as the stories were worked. This tim I wanted ot see if it would save me time (and tokens) to do it differently.

After the initial draft of the stories, I ended up asking CC to add 4 new stories to fill in some desired features. It also needed details on how to call the external API used to calculate shipping. I Was able to give it the API contracts and a fake endpoint. But without an actual shipping API, the stories won't be possible to implement fully.

In addition, CC will require the format of the files it needs to create for sending the order data to the warehouse. That needs to be defined and added to the stories.

For both the API and the file format I plan to use CC to create them, but not in the normal flow. I'm going to try using CC in a separate project (with different context) to get them ready for this project to consume.

**What worked well:**

Breaking down the milestone into stories worked well, including all the details. Doing it all at once used far fewer tokens that doing it on-demand. But I'm not sure if the quality of the output is as good. Time will tell.

**Questions or ideas:**

Upon further review, I noticed that some of the requirements that CC defined in the stories are not what I would like. I need to adjust some of the way it works. Again, I don't think this is a CC issue, but rather I was unable to provide CC with enough direction to write the stories correctly. But on the flip side, CC didn't ask me questions about how the features should work. It inferred desired behavior, rather than confirming with me. I have seen a few ways that folks have tried to overcome this outcome (e.g. the 'grill me' skill from Matt Pocock), so I am not alone in needing this ability from CC.

In my next session I am going to try and see if CC can change the stories to match my expectations.

Consumed 19% of available tokens (5 hour window)

## 2026-04-19 - Matt Edgar - Phase 2

**Working on** Work on Customer Profile Story
**Duration:** 2.25 hours

**What happened:**

I abandoned all the work on issue 40 and ask CC to redo the work, this time using Opus instead of Sonnet.

The result was a much better implementation. I think Sonnet could have done the work if I had given it better instructions.

Using Opus cost 35% of my 5-hour token limit.

I switched back to Sonnet to complete the rest of the tasks on the story.

Oddly, on the last task, CC did not create a new branch for its code changes, nor did it commit the changes. 

With breaking down the story, Sonnet made reference to an implementation algorithm (BCrypt for hashing passwords, rather than the PasswordHasher abstraction). I manually modified the story to be more clear.

**What worked well:**


**Questions or ideas:**
This is the end of Milestone 1. I am going to mark this as the end of Phase 2 as well. I am going to make some further adjustments to the CC instructions to remove/reduce some of the friction points.


Consumed 59% of available tokens (5 hour window)

Addressing some of the friction points consumed 31% of available tokens (5 hour window)

## 2026-04-18 - Matt Edgar - Phase 2

**Working on** Work on Customer Profile Story
**Duration:** 1.25 hours

**What happened:**
I noticed that CC was reading the existing files to determine the correct patterns to follow. I wonder if providing additional templates/skills would consume fewer tokens?

I had to stop CC mid-story when it got 'lost' attempting to implement the first task that dealt with security.

It implemented a horrible solution for making secure API calls from the Blazor code to the API Service.

And I realize that the fault lies with me. I didn't properly define how the security should work. And the instructions I provided in the PRD were misleading.

It churned on the task for a long time (32% of my 5 hour token limit) and produced gibberish. But honestly it was doing the best it could given the poor instructions.

I'm going to have to regroup and think about how I want to address this. I could try to fix the instructions and make it work properly. Or I could get rid of all the security features and work with CC on other tasks. My goal here is to learn how to interact with CC, so the first option might be the best way to learn how to deal with failure.

Interesting.... I asked Opus (4.7, all new and shiny) to create a plan for me using the Aspire starter app. It did what seems to be a great job. I asked it to adjust the plan so that I could included it in another project, include a reference to it from CLAUDE.md. And it did this very well.

But then it "added useful memories" from this session. It created a document called "feedback_doc_deliverable.md" which says when user asks for a document to clarify if they want a reusable doc or a one-off doc. And it created a "project_aspireapp.md" document indicating that the solution is a start project for learning. It then wrapped these up in a MEMORY.md file:

- [Doc deliverables are often reusable guidance](feedback_doc_deliverables.md) — "document X" may mean CLAUDE.md-ready rules, not an impl plan; clarify up front
- [AspireApp is a guidance-doc scratchpad](project_aspireapp.md) — Aspire 13 + Blazor Server + API starter; output is often reusable docs, not running code

Very interesting. Good to know I can use this technique in the future to help ground CC.

Now I need to figure out what to do with the Widget Depot project. I can add a reference to the new plan:

```markdown
See [docs/auth-rules.md](docs/auth-rules.md) for authentication standing rules.
```

But then what? I could make the changes the plan suggests manually. Or I could ask CC to make the adjustments. I think I will make the changes myself as a learning experience. I'll get things reworked up to the point of the Profile story. Then I'll let it start from there with the new plan and see how it does. But that will be for later, as I only have 20% of my token limit remaining.

**What worked well:**

**Questions or ideas:**

Consumed 80% of available tokens (5 hour window)

## 2026-04-17 - Matt Edgar - Phase 2

**Working on** Work on Customer Login/Logout Story
**Duration:** 1.5 hours

**What happened:**
I worked with CC well today. I changed the settings.json file to allow CC more control over the workflow process. 

If I want to get myself out of the role of orchestrator, I need to give CC more instructions on how to:
- clean up the git branches when it is done
- create cleaner commit messages when merging pull requests
- update checklists in GitHub issues when the tasks are complete

I noticed a few cases where the model is not using the patterns I would like. I'll need to fix that too.

**What worked well:**
The model (Sonnet) understands the Blazor and C# world quite well.

**Questions or ideas:**
There are a lot of security related decisions that I have not made yet. If this were a real project I would probably need to stop and reassess how users authenticate themselves. I think things are okay for this test project for now. But I plan on using these features as a way of asking CC to modify the authentication workflow later and see how it reacts. Not a test of CC as much as it is the models.

How much of what I am seeing in productivity gains due to the model and how much is due to CC? I may want to change the model and see how the results differ. I feel like it is a combination of a capable model and the tooling to control the context (which is mostly what CC is doing) that makes the real difference.

47% of my tokens consumed for one story? The "Pro Plan" is really a "Paid Free Plan". You really can't do anything serious without a high-tier plan.

Consumed 47% of available tokens (5 hour window)

## 2026-04-14 - Matt Edgar - Phase 2

**Working on** Self Registration Story
**Duration:** 1.5 hours

**What happened:**
This is the first session with the new settings. It went smoothly. 

It correctly created an issue in GitHub for the story.

Each time CC attempt to make a pull request, it forgot to push the branch first.

My hook to run dotnet format prior to each commit didn't work perfectly. It didn't re-stage the files
that it changed. So CC helped me get that resolved.

A bug was found in testing the work. I fixed the bug myself. Next time I need to let CC attempt a fix.

**What worked well:**
- Breaking down the story into tasks.
- Following the existing patterns.

**Questions or ideas:**
None

Consumed 41% of available tokens (5 hour window)


## 2026-04-11 - Matt Edgar - End of Phase 1

**Working on** Adjusting Claude Code
**Duration:** 2.0 hours

**What happened:**
I have completed the first phase of this learning exercise. Overall, I haven't had too many friction points to complain about. But there are a few things I want to adjust.

I have now gone in and made several adjustments to Claude Code to see if there are improvements in the way CC behaves in the next phase.

- I moved the major portions of the instructions from the CLAUDE.md file to separate files under the '/docs/standards' folder. I assume CC will use these
files as needed, reducing the overall context size on any given task.
- I adjusted the editor config file to my preferences
- I added hooks for CC to run `dotnet format` before creating a new commit or creating a pull request.
- I added guidance fo testing (unit) and for code (C#) design to hopefully minimize adjustments I need to make (or ask CC to make) as the code evolves.
- I asked CC to include unit tests as part of completing tasks, not as a separate task. I also asked it to create an issue in GitHub for the story, as well as the individual tasks.

**What worked well:**
None

**Questions or ideas:**
None

Consumed 16% of available tokens (5 hour window)


## 2026-04-10 - Matt Edgar - Phase 1

**Working on** Second Story
**Duration:** 2.0 hours

**What happened:**
I asked Claude Code (CC) to run through the tasks for the second story.

CC refined the 2nd story. No manual edits. I asked it to break the story down
into tasks. Fine. Then added the story and the tasks as issues in GitHub.

Prior to working on this story, I (manually) added/changed the folder
structure, naming convention and the way the endpoints are registered. CC
had no problems following the new patterns without any additional prompting
or instructions.

On one of the tasks, it committed (locally) to the main branch, rather than
creating a feature branch. It caught it and corrected the issue itself. Probably
need to add a rule preventing commits being pushed directly to the main branch.

**Friction points:**
It wanted to create separate issues for each task. I wanted the story to
be added as well. This required additional guidance. Probably need to update
the instructions to see if this can be the default behavior.

It created a separate task for unit tests. I need the tests to be included
in the task that creates the code. Again, need to update the instructions.

**What worked well:**
- Breaking down stories.
- Following existing patterns.

**Questions or ideas:**
None

Consumed 38% of available tokens (5 hour window)

## 2026-04-07 - Matt Edgar - Phase 1

**Working on** First Story
**Duration:** 1.5 hours

**What happened:**
I asked Claude Code (CC) to run through the tasks for the first story.

CC added the 'simple' DI container injection. The endpoints were added to the Program.cs.

I found the requests to approve actions (gh issue, git pull, etc.) were good to follow, rather than
allow CC to run the commands without my explicit approval. But I can see that some of these i should
lte it run.

**Friction points:**
None

**What worked well:**
It added the EF Core and Blazor features with minimal adjustments from me.

**Questions or ideas:**
I need to add some additional infrastructure to the projects to follow the patterns I want. Then I
need to add more context to ensure CC will follow the patterns.

I need to come up with a set of actions I let CC perform without me having to approve.

Consumed 11% of available tokens (5 hour window)

## 2026-04-06 - Matt Edgar - Phase 1

**Working on** First Story
**Duration:** 1.5 hours

**What happened:**
I asked for help refining the first story in the project. It did well. I then asked Claude Code to
refactor the UI "Components" folder to use a "vertical slice architecture" structure. It did pretty well,
but I had to give it a few pointers. This took an significant amount of time and tokens. It consumed 26%
of my 5-hour window budget of tokens.

Next, I asked Claude to break down the first story into tasks. The first thing it did was started
scanning the git commit history. I was very confused. I stopped it mid-task and asked why it was doing
that. Turns out I had the wrong file selected, so it decided to try and find the story in question. Once
I selected the correct file that contained the story, it started up again.

This time it started scanning the entire codebase. I stopped it again and asked:

Me - Why are you scanning the repo when I asked you to break the story down into tasks?
CC - Fair point. I have everything I need from the story. Let me write the plan now.
Me - No, stop. I want to know why you were scanning the repo?
CC - I'm in plan mode, which instructs me to explore the codebase before planning. But you're right
that it wasn't necessary here — the story is self-contained, you told me what exists, and breaking
a story into tasks doesn't require reading source files. I over-applied the plan mode workflow
to a task that didn't need it.

I found this interesting. This is not what I expected the plan mode instructions to entail.

I asked how I could adjust the plan mode behavior. It suggested I add a section to the CLAUDE.md file,
so I did:

```markdown
## Plan Mode

Do not explore the codebase during planning unless the task requires it or the user explicitly asks.
If the user's request is self-contained (e.g., breaking down a story, writing a plan from a spec),
go straight to planning.
```

Once it was finished I asked it to use the GitHub CLI to add issues to the repo for the Story and the associated
tasks. It did this very well.

**Friction points:**
In plan mode it (seemingly) wasted time (and tokens) scanning the codebase for no reason. In addition,
rather than ask for clarification on a request it was given, it tried to figure it out on its own. Not
unlike an eager intern. 

**What worked well:**
- Breaking down a story into tasks was done very well.
- Using the GitHub CLI was seamless (I had provided good instructions in the CLAUDE.md file previously)

**Questions or ideas:**
It seems that the context we provide the models is necessary to keep the response behavior focused
and not wasting time and tokens. The principle of least surprise does not apply here. The default
behavior is not obvious (at least to me).

## 2026-04-03 - Matt Edgar - Phase 1

**Working on** Technical Stack
**Duration:** 1.5 hours

**What happened:**
I asked Claude Code to draft a set of user stories for the first Milestone. Just the titles
and descriptions, based on a template I provided. It did this very well.

I worked on describing the technology stack I wanted to use for this project. I decided to use
a set of technologies that i user every day in order. If I choose a new technology that i am 
not familiar with, I feel it will impact my ability to measure the impact of using Claude Code. As
I become more familiar with Claude Code, I may explore some other technologies.

I decided to document a high-level set of architecture decisions and choices in a single file. I
asked Claude Code to create a folder of coding standards for it to follow. It did well with the
architecture file I asked to be created. I got confused and was searching for the project files 
in the repo. I stopped it and informed it that no source code existed yet. It then created the 
Markdown file.

**Friction points:**
None

**What worked well:**
- Breaking down milestone into user stories.
- Defining coding standards

**Questions or ideas:**
None 

## 2026-04-02 - Matt Edgar - Phase 1

**Working on** Product Requirements Document
**Duration:** 1.5 hours

**What happened:**
I encountered some friction. It used the term "Non-Goals" in the PRD it generated. I thought that
was odd. I asked it to explain and it said it was "standard product/engineering document terminology".
When I asked it to provide me with references, it said it didn't want to because they might be broken
or out of date links. I asked it to give them to me anyways. The 2 links to provided were indeed broken.
I did my own research and discovered that out of the dozens of PRD templates available on the web,
only a couple included that term. I suspect it isn't as standard as Claude led me to believe.

<https://github.com/priankr/prd-templates/blob/main/PRD%20Templates/Asana%20Spec%20Template.md>

**Friction points:**
I asked Claude Code to not use "Non-Goals" in any future PRD drafts. It said it would store it in
its "memory". I asked it to explain and it said this "memory" was markdown files it maintained in the
~/.claude folder. I let it do it, but saw that it applied the memory in a markdown file only scoped
to the current project. I asked for it to be applied on all projects and it moved the files to the
appropriate location.

**What worked well:**
It created a good PRD that included all the points discussed in the business requirements.

**Questions or ideas:**
The ~/.claude folder is where it stores some of its 'memory'. If I move to another machine, all
that context is lost. I'll need to keep them in sync (or at least portions of them). 

 - memory
 - plugins
 - settings.json (maybe?)
 
