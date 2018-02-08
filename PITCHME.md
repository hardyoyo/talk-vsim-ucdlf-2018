# VSim
## Getting the job done with DSpace
## while avoiding all the traps of customization

Hardy Pottinger

Digital Library Software Developer, UCLA Library

@fa[twitter] @hardy.pottinger

@fa[envelope] hpottinger@library.ucla.edu

---
# What is VSim?

---
https://vsim.library.ucla.edu/

VSim is a desktop software application for navigating and augmenting 3D architectural models

> ... a simple-to-use interface for exploring computer models of historic sites and environments. Designed to support both teacher-centered presentations and student-centered assignments.

Note:
VSim is 2 things: it is a desktop application for exploring 3d models, and a repository or archive of those models and related files

---
https://vsim.library.ucla.edu/

VSim is also a *repository* of 3D architectural models

> ...preserves academically generated models for use in both formal and informal educational settings. Scholars across the country have constructed these models to exacting standards, so they are ideal teaching and learning resources.

---
# VSim: we have use cases and design docs
---?image=assets/images/lots-of-em.png&size=auto

Note:
Like all big projects, we have many design artifacts to guide our way. Out of all these materials, the key to understanding what we needed to build was the object model.

---
# VSim: proposed object model
---?image=assets/images/vsim-object-model.png&size=auto

Note:
This is a sketch, I'll show a more refined version in a few minutes.

---
# The story of VSim
## from Hardy's Perspective

Note:
* I'm a DSpace committer
* I was hired at UCLA Library in August of 2017, my first big project: VSim
* VSim use cases and design documents describe what amounts to a standard repository site
* LET'S USE DSPACE!

---
# What is DSpace? tl;dr
* wikipedia.org/wiki/DSpace
* youtube.com/user/dspacedirectvideos
* youtube.com/watch?v=7dSNuBfTYeo
* wiki.duraspace.org/display/DSDOC6x/Functional+Overview
* www.wiki.ed.ac.uk/display/datashare

Note:
I can say a lot about DSpace, and I have a few more slides ready if anyone wants me to do so, but we'll skip them for now, to get on with the story. Where were we? Oh, yeah, data models.

+++
# What is DSpace?
* community-driven open source repository software
* a *Java Servlet* - requires a servlet container, like Tomcat, Jetty, JBoss, GlassFish
* a set of Java-based *utility scripts*

+++
# What is DSpace?
* an *asset store* (filesystem or service) and
* a *metadata store* (PostgreSQL or Oracle)

+++
# What is DSpace?
* the most widely used repository software platform (open source or proprietary)
* about 2,000 installations worldwide (120 countries)
* 70% of all institutional repositories (according to an ACRL survey) run on DSpace

+++
# What is DSpace
* a very active community of developers, managers, and users, across the globe (19 active committers, over 150 contributors on GitHub)
* developers: dspace-devel@googlegroups.com
* managers: dspace-community@googlegroups.com
* tinyurl.com/dspace-dcat
* users: dspace-tech@googlegroups.com

---
# DSpace Data Model

---?image=assets/images/DSpaceDataModel.png&size=auto

Note:
We've got three major kinds of things here: items which contain bitstreams, collections which contain items, and communites which contain collections.
This might look familiar, if you've worked with the Portland Common Data Model, the DSpace model pre-dates PCDM, and isn't nearly as flexible.

---
# DSpace Data Model
* this data model is "baked in" to DSpace
* you can't really change it or customize it
* but you *can* give it a "fancy coat of paint"
* i18n customization allows you to change any text you wish, on any page of DSpace
* example: "collection" can become "project"
---?image=assets/images/VSimDataModel.png&size=auto
Note:
Each project will be a community, with three collections (vsim files, archives, and community submissions). This sums up the approach we started to pursue after discussing the limitations of the DSpace data model. Seems reasonable, right? Only, there's a problem.
---
# Metadata Problem
only one type of object in DSpace can have customized metadata

![DSpace Item](assets/images/DSpaceItem.png)
---
# DSpace Items
## Have Qualified Dublin Core metadata
```
dc.contributors
dc.contributor.author
dc.date.acessioned
dc.date.issued
cd.identifier.uri
dc.description
dc.description.abstract
dc.title
dc.type
```
---
# DSpace Items
## Can *also* have bespoke DC-like metadata
```
vsim.acknowledgements
vsim.bibliography
vsim.continent
vsim.contributor
vsim.keywords
vsim.news
vsim.peerreview.agency
vsim.peerreview.status
vsim.relation.archives
vsim.relation.community
vsim.relation.models
vsim.relation.projectMaster
vsim.relation.submissions
vsim.reuse.submissions

```
Note:
So, we had a dilemma: we had all this metadata specific to projects that we wanted to include, but the only thing that DSpace would allow us to customize (without major code changes) was DSpace items. Before giving, up, we decided to see if we could make it work. And we came up with an idea of...
---
# A ProjectMaster Item
## One item to rule them all!
* all Vsim projects are entered as items in a special collection, called VSim Project Masters
* all other containers required by the VSim archive are derived from these master items
* a series of custom curation scripts make all the magic happen
---
# DSpace Curation
* provides a way to manage routine content operations on a repository
* designed to encourage local extension
* https://tinyurl.com/dspace-curation
> This gives DSpace sites the ability to customize the behavior of their
> repository without having to alter... the DSpace source code.

Note:
Sounds great, right? One small problem...
---
# Curation scripts stop working if the object changes state
* DSpace items in a submission workflow are different than DSpace items archived
in a repository
* The curation system will happily *try* to shepherd an item through the transition
from a workflow item to an archived item, but it will fail, quietly.
* This is a bummer
---
# Surely somebody has fixed this, right?
* The DSpace community is *full* of people who wrestle with quirky issues
* One just has to ask for help, on a mail list or in a chat room
* Or in person, at a conference, where they are presenting on their solution to
this exact problem
https://or2017.net/wp-content/uploads/2017/06/243.pdf
---
# IRR Team at ITS, the University of Waikato
* https://uow-irrs.github.io/
* https://tinyurl.com/dspace-queue-task-on-install
Note:
The developer presenting the poster was my friend Dr. Andrea Schweer, a fellow DSpace committer. In the past, whenever I've found out Andrea had a solution to a problem I had encountered, I would have to beg for weeks or months for her to share her code with me. This time was different, she had the code ready to share, and had built a whole site around sharing many of her customizations to DSpace. I recommend exploring that site there, if you work with DSpace at all, there are many treasures on that site.
---
# The rest is just details

@fa[github] [github.com/uclalibrary/dspace/tree/ucla-vsim-6_x](https://github.com/uclalibrary/dspace/tree/ucla-vsim-6_x)

@fa[sign-in] [vsim.library.ucla.edu](https://vsim.library.ucla.edu/)

@fa[twitter] @hardy.pottinger

@fa[envelope] hpottinger@library.ucla.edu

slides: [github.com/hardyoyo/talk-vsim-ucdlf-2018](https://github.com/hardyoyo/talk-vsim-ucdlf-2018)
all infographics created with [yEd Graph Editor](https://www.yworks.com/products/yed)
using [yed-aws-palettes from Abesto](https://github.com/abesto/yed-aws-palettes)

note:
Sorry for such a hand-wavy ending. Seriously, if you're interested in finding out more about how we modified DSpace the code is all on Github. I've covered the unique things we've done, and how we made the changes with an eye towards avoiding altering the source code. I really like how we've used curation scripts to add on additional business logic. Those scripts should continue to run in future versions of DSpace. The remaining changes we've made are all standard DSpace kinds of things: front-end theme work with CSS and jquery, configuration. We borrowed some code from 4Science in Italy, to look up values from the Getty Thesaurus of Geographic Names. And we borrowed a patch to display the value of a contributor's Orcid, if we have it. But, those are just details, you're intested you can look at our code.

We have a couple of minutes for questions, if you don't get a chance to ask me now, stop me in the hall, or there's my contact info, send me a note.
