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
https://vsim.library.ucla.edu/xmlui/

VSim is a desktop software application for navigating and augmenting 3D architectural models

> ... a simple-to-use interface for exploring computer models of historic sites and environments. Designed to support both teacher-centered presentations and student-centered assignments.

---
https://vsim.library.ucla.edu/xmlui/

VSim is also a *repository* of 3D architectural models

> ...preserves academically generated models for use in both formal and informal educational settings. Scholars across the country have constructed these models to exacting standards, so they are ideal teaching and learning resources.

---
# VSim: we have use cases and design docs
---?image=assets/images/lots-of-em.png&size=auto

---
# VSim: proposed object model
---?image=assets/images/vsim-object-model.png&size=auto

---
# The story of VSim
## from Hardy's Perspective

* I'm a DSpace committer
* I was hired at UCLA Library in August of 2017
* VSim use cases and design documents describe what amounts to a standard repository site
* LET'S USE DSPACE!

---
# What is DSpace? tl;dr
* wikipedia.org/wiki/DSpace
* youtube.com/user/dspacedirectvideos
* youtube.com/watch?v=7dSNuBfTYeo
* wiki.duraspace.org/display/DSDOC6x/Functional+Overview
* www.wiki.ed.ac.uk/display/datashare

---
# What is DSpace?
* community-driven open source repository software
* a *Java Servlet* - requires a servlet container, like Tomcat, Jetty, JBoss, GlassFish
* a set of Java-based *utility scripts*

---
# What is DSpace?
* an *asset store* (filesystem or service) and
* a *metadata store* (PostgreSQL or Oracle)

---
# What is DSpace?
* the most widely used repository software platform (open source or proprietary)
* about 2,000 installations worldwide (120 countries)
* 70% of all institutional repositories (according to an ACRL survey) run on DSpace

---
# What is DSpace
* a very active community of developers, managers, and users, across the globe (19 active committers, over 150 contributors on GitHub)
* developers: dspace-devel@googlegroups.com
* managers: dspace-community@googlegroups.com
* tinyurl.com/dspace-dcat
* users: dspace-tech@googlegroups.com

---
# DSpace Data Model

---?image=assets/images/DSpaceDataModel.png&size=auto

---
# DSpace Data Model
* this data model is "baked in" to DSpace
* you can't really change it or customize it
* but you *can* give it a "fancy coat of paint"
* i18n customization allows you to change any text you wish, on any page of DSpace
* example: "collection" can become "project"
---
# Wait, you said the DSpace object model can't be changed?
How did you ever git VSim data to fit the DSpace object model?
---?image=assets/images/VSimDataModel.png&size=auto
---
# Ooops, metadata problem
* Only one type of object in DSpace can contain customizable metadata
![DSpace Item](mage=assets/images/DSpaceItem.png)
