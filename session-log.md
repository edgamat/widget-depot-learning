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
 
