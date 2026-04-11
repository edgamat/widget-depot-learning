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
- I added guidance fo testing (unit) and for code (C#) design to hopfully minimize adjustments I need to make (or ask CC to make) as the code evolves.
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
 
