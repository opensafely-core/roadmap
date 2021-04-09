# Vision

There are many versions of our vision lying around in various documents. Until we have crystallised on one, this document takes the following definition:

> OpenSAFELY exists to improve the security, quality, reproducibility, and accessibility of clinical and epidemiological research and analytics.
>
> It does so bringing best practice software engineering techniques such as continuous integration testing and code reviews to research software practice.
>
> It encourages open, transparent ways of working through careful system and user interface design, and by enabling a positive and supportive culture around the platform.
>
> It encourages secure and responsible treatment of patient data. It does this by systematically minimising the use of patient data by design, at every stage of a project's life.  It also provides assurances to the public through open and transparent audit trails of how and when patient data has been used.

The prototype stage will be considered complete when the platform:

1. Has **public dashboards** that demonstrate the progress of individual projects from conception, through approvals and development, to completion and publication; including the ability to track which data is subject to which information governance approvals
2. Has **50 completed, shared, external analyses**
3. Has a range of **GUI-driven workflows** that can generate non-disclosive outputs **without manual intervention**
4. Has a **variables library** with at least 20 variables: reusable, audited code+data components that can be selected and incorporated into stuy definitions
5. Has an **actions library** with at least 10 actions: reusable pipeline actions that transform input data into commonly-used outputs, such as crosstabs and visualisations
6. Has sufficient **tooling and documentation** to allow a **third party** to write, run, and maintain their own backend, and three such backends running
7. Has a **peer support community** that can operate without Datalab staff involvement
8. Has a fully documented and audited **privacy infrastructure**

There are headings below for each of these goals. Our aim is to complete these by April 2023.


# 1: Public dashboard

The public dashboard has three objectives:

1. Provide accountability to our funders, to whom we proposed the key metrics of 10 completed, shared, external analyses by (approximately) November 2021; and fifty by November 2023
2. Hold researchers accountable to the values of transparency, quality, and to their ethical duty to complete their research
3. Give the public confidence that their private data is being used responsibly and for valuable purporses

All subsequent roadmap items can be viewed through this lens: “How does this effort contribute to the number of completed, open, published analyses?”

One way of implementing this dashboard is with the "sales funnel" metaphor. This would make it easy to visualise the quantity of researchers at each stage of the funnel. Key funnel stages could be the points when the user:

1.  expresses an interest by emailing us
2.  firms up their interest by registering their github account with OpenSAFELY
3.  demonstrates basic skills by completing the tutorial
4.  applies to use the platform for a specific project
5.  receives approval to use the platform
6.  has initial planning and support meetings with OpenSAFELY onboarding team
7.  runs any code against real data
8.  completes proxy quality metrics (e.g. number of projects with code reviews, green GI ticks)
9.  has any outputs published
10. makes their repo public
11. publishes material which references their repo

All these aggregate numbers should be public on our website.  Individual organisations might get breakdowns by project.

The same sales funnel process could, over time, grow a workflow to support the onboarding/support team in deciding how to schedule internal support resources, prioritise approvals, etc.  For example, an organisation with a proven track record of publish research with OpenSAFELY might get their outputs checked for release at a higher priority than an organisation without this record.

The public should be able to see a list of published projects, publications related to each project, and to be able to access code related to each publication. Each project will have one or more Data Sharing Agreements. These should be visible on each project page.

This implies incorporating information governance approvals into our onboarding data model ([ticket](https://github.com/opensafely-core/cohort-extractor/issues/172))

# 2: Fifty completed, shared, external analyses

To achieve this, we need to:
* Make it easy for people to find out about the platform
* Give people reasons to use the platform
* Avoid giving people reasons to leave the platform early

Some of these goals are covered in detail further down the page under different headings.

To **make it easy to find out about the platform**, we should:

* Create a constent and recognisable **brand** across all our websites (currently: documentation, job server, project website)
* Produce a range of high-utility, **automated data reporting services** to the **NHS analytics community**; for example Service Restoration Observatory (SRO) dashboards at regional, STP, and PCN geographies, modelled on the OpenPrescribing pattern. These would be published on our own **Short Data Reports website**, in public where possible, and behind a password where politically necessary.
* Produce a similar range of **automated data reporting services for the research community** around variables and data quality; for example, the prevalence and strengths and weaknesses of available "Care Home" flags in EHR data. These could be on the same Short Data Reports website.
* Allow study developers to assert authorship of **openly-licensed, citable components**, such as codelists, variable definitions, and actions
* **Write blogs** for research and sofware engineering audiences; **present at conferences**; **write papers** about methods.
* **Require attribution for OpenSAFELY** in a consistent and preferably prominent manner

The reasons people might **want to use our platfor**m rather than any other include:

* **Batteries included**: GUI-driven workflows (q.v.),  **actions library ** for common patterns, pre-validated study **variables library**
* A friendly, inclusive and **welcoming brand** and community experience
* An interest in open science, and therefore **using an open source framework**
* A desire to learn about improving the quality and reproducibility of their research, i.e. **career advancement**
* **Acquiring credit** through reusable components
* The fact they get **simple parallelisation**: this is unlikely to be part of their current workflows
* In some cases, we might remain the only way to access certain datasets, but that is increasingly unlikely as more TREs proliferate

The reasons people might **leave the platform early** include:
* **Too difficult to get to the first output**. Tasks to remedy include:
  * intensive iteration on our getting started guide to get it down to a 20 minute end-to-end process
  * making reliance on Docker optional, by providing a remote-run service
  * providing an opensafely-cli installer, so people don't need to install python first
  * improving our documentation, including linux and macOS-specific instructions
* **Complicated onboarding ceremony**, particularly around information governance. Tasks to remedy include:
  * Writing a web-based onboarding workflow/FSM with automated transitions that assign roles, etc (in progress). Administrators should always be able to see what their next steps are.
  * Surfacing onboarding progress clearly for applicants. Users should always be able to see where they are in the applications process.
  * Very clear documentation of onboarding process, with expected timescales, justifications, etc
* **Difficulties of iterative, local-only development** when you have to largely work with dummy data. Tasks to remedy:
  * Ability to provide your own dummy data
  * Better built-in dummy data defaults, perhaps based on real prevalences
  * Rules-based dummy data generation for power users
  * Fast local execution of the pipeline; more importantly, fast execution in CI tests
  * Users are loathe to create public codelists in opencodelists during the iterative phase. There should be a way to support draft codelists - [discussion here](https://github.com/opensafely-core/job-runner/issues/18).
* **Awkward edge cases for development**
  * In particular, to take advantage of parallelisation, users currently have to do lots of copy-and-pasting in their `project.yaml` to repeat actions with different arguments. There's [a proposal to introduce "matrix" functionality to the config](https://github.com/opensafely-core/job-runner/issues/124).
* **Poor performance or availability** which slows down progress. Tasks to remedy:
  * Understandable, fair and flexible resource scheduling, with predictable failure modes. The user experience at the moment is that a single massive project of many long-running processes can hog all the resources, so others' jobs can take an unpredictable amount of time to be scheduled. We have a super-naive manual override at the moment for handling the most egregious cases.
  * Surfacing of resource usage to end users in easy-to-interpret format (for non-technical users)
  * Thinking about our internal availability targets, in particular around the job server, but also the backends we run
* Complicated or slow processes for **assuring non-disclosive publication of data**. Tasks to remedy:
  * Placing onus on researcher to minimise releases and describe them clearly, and document this in `project.yaml`
    * Providing actions which make low number suppression easy to carry out, and easy to demonstrate it has been carried out
  * Documenting our release process and making it predictable and understandable to users (currently: you get two releases for free, pay for subsequent ones, we do it once a week on a specific day, fill out this google doc first)
  * A user interface for reviewers which supports easy viewing, redacting and annotating of outputs
  * A user interface for publishes to support simple publication
  * An output viewer integrated into the job server which allows study authors to publish outputs to selected audiences prior to full publication
  * The ability to publish finalised outputs as release artefacts to the github repo, so it's all archived in one place

### Dummy data

There are considerable limitations and problems with the current expectations/dummy data model. For the time being, this is as good a place as any to record several tickets on the subject:

Bug reports:
* [Expectations data does not respect inclusions criteria](https://github.com/opensafely-core/cohort-extractor/issues/359)
* [Expectations data does not respect `aggregate_of` covariates](https://github.com/opensafely-core/cohort-extractor/issues/404)
* [There should be an RNG seed for expectations](https://github.com/opensafely-core/cohort-extractor/issues/507)
* [Date expectation required even if not returning any dates](https://github.com/opensafely-core/cohort-extractor/issues/350)
* [No expecatations data available for vaccinations in TPP](https://github.com/opensafely-core/cohort-extractor/issues/428)
Proposals (required reading!):
* [A generic model for encoding arbitrary relationships between random data](https://github.com/opensafely-core/cohort-extractor/issues/221) (lots of excellent discussion here)
* [Allow simple co-variation of variables via a DSL](https://github.com/opensafely-core/roadmap/discussions/9) (this is like a simplified version of what's proposed in the previously-linked ticket)
* [Allow users to generate their own dummy data](https://github.com/opensafely-core/roadmap/discussions/7)
https://github.com/opensafely/cohort-extractor/issues/404
* [Dummy data population size should live on study_def rather than in project](https://github.com/opensafely-core/cohort-extractor/issues/346)
* [Provide canned distributions for common categoricals in expectations](https://github.com/opensafely-core/cohort-extractor/issues/312)

I believe the correct iterative approach to improving this to start by allowing generic, custom dummy data generation, then to re-implement expectations as one way of providing that, then to implement other DSLs for different use-cases.

# 3: GUI-driven workflows for happy path

We need a powerful story to tell that will impress decision-makers and researchers alike.  Here are two for starters:

## User story: clinical lead generates custom measures

A clinical lead in an STP wants to know the prevalence of COPD in their area, stratified by age.

They have found out that this is easy through our Short Data Reports website; the Datalab has created dashboards for various Service Restoration Observatory measures that are public at a national level, and has local breakdowns for their own STP behind a login.  They found this because a colleague sent them a link to it.  On the page, they saw a breakout box explaining that with the appropriate permissions, they can create their own measures. They follow the link to a short guide, which walks them through the following process.

They visit the variables library to find that there are several existing definitions of COPD (all based on codelists). They pick the one which is listed as having had the most citations; they are reassured to see that this variable includes citations a few from well-known universities, and they can see that there has been a clinical review in the last 24 months.

On the COPD variable page they've chosen, there is a "generate measures for this codelist" button. When they click the button, they are warned that they are not logged in or approved, so can only generate measures (with dummy data). They continue, and are taken to a page with a series of dropdowns that allows them to filter the data down to their own STP, to group by age band, and to request the last 12 months of data, by month.

They press a "generate measures" button, and see a spinner. After a few seconds (it's fast because it's dummy data), they see a deciles chart and a data table summarising the outputs. There is a notice explaining that this is random data; in order to generate real data they will have to request IG approvals.

They click on a link to start the IG process. They are presented with a form asking them for details of their project. They are told they can expect approval within the next 20 working days.  They are finally asked to create a Github account and sign in with that, to complete the process.

When they receive an email 20 days later containing IG approval, it includes a link to log into the opensafely website, where they can still see the dummy project they created before. There is now a new option to run it against the TPP and EMIS backends. The user selects both, and are told they'll receive an email when the data is generated. They can expect this to take a few hours.

When they receive an email, they can follow a link to see the aggregated, low-number suppressed data. They are encouraged to press the "publish" button to make it public; they are also given an option to repeat the report generation once a month.

## Implied features

The above story implies a number of major new features not yet in the platform:

* A short Data Reports website with actionable measures at an STP level
* A citable variables library, built on top of opencodelists
* A UI for generating a measures-based study definition and actions pipeline
* The ability to generate outputs from dummy data in the job server
* An outputs viewer embedded in the job server
* Better dummy data so the random data doesn't produce confusing outputs
* A web-based IG approvals workflow
* What follows from this is the need for a mechanism to mark a certain state of code as safe. This needs (a) some kind of security against code injection or other MitM attacks e.g. cryptographically signed git commits or docker images, (b) a registry of known-safe signed code states, (c) a simple-to-follow process for new releases of the code (e.g. diff to previously known-safe code, checklist of things to look out for, signoff by two people)
* A job scheduling function
* The ability to combine known-safe measures data from two backends

## User story: researcher carries out simple regression

A researcher wants to investigate factors associated with long covid.

They start by browsing the variables library to see what variables are already defined.

They find variables for all the factors they are interested in: a "long covid" variable, age in ten year bands, sex, IMD, and ethnicity. They add these to a "shopping basket".

When they have finished, they review the "shopping basket". They fill out a field asserting which (already-approved) project this is part of, and an id and title for the repo. They also fill out fields which define the population they're interested in: in this case, all patients registered in one practice during 2018. They click "create a new study".

After a short time, they see a page telling them a new repo has been created (with a link to Github), which includes a study definition and a pipeline that extracts the cohort, and runs a study report. They are prompted to request that the study report be run, as this will give them useful initial information about their cohort.

They click this button, and are told to await an email confirming the outputs have been created.

A couple of hours later, the jobs have completed, and they follow a link in the email that takes them to the cohort report, which has been automatically published.

They are now ready to start writing code. They follow the link to their Github repo, clone it, and run `opensafely run_all`, which generates representative dummy data for them to work locally.

##  Implied features

All the features from the previous user story, plus:
* A "shopping basket" interface that allows you to build up elements of your study definition interactively
* A user interface for definition a patient population based on fields in the shopping basket
* A means to generate a study definition from this UI-based specification

We might also consider if being able to round-trip between a hand-coded study definition and a UI representation might be desirable.

# 4: Variables library

A variable (this possibly needs a better name; some call this a *phenotype*, but we don't like that) is the combination of one or more codelists, and zero or more sets of conditional logic.

The simplest example would be `age_in_years`, which is self-explanatory.  An iteration might be `age_in_ten_year_age_bands`.

A more complex variable might be a diagnosis of aplastic anaemia, which is coded using one or more of at [least 60](https://codelists.opensafely.org/codelist/opensafely/aplastic-anaemia-snomed/2020-04-24/#full-list) possible SNOMED codes.

The most complex variables are algorithms for determining state based on a number of possible conditions. For example, ethnicity can be inferred from more than 20 SNOMED codes, each of which may be repeated a number of times for each patient, and in a number of different data sources. A single data source can give conflicting information about a patient, as can different data sources. A suitable algorithm combines selecting codes, reducing them to smaller sets, and resolving conflicts between different accounts of the truth. At the moment the implementation of a single variable is spread in several places - the codelist(s), Github tickets discussion the implementation, `categorised_as` code in a study definition.

The variables library is likely to be based on the existing opencodelists tool; it will need a way to incorporate the kind of logic described above, which is currently expressed only in study definitions. Ideally, there would be support to use the library website as an authoring tool, but the pragmatic solution may be that people author the logic by hand in a study definition (much as they currently do) and copy across code snippets to the variables library when they're happy.

Variables should show an audit trail for users to trace clinical reviews. They should be easily citable, and where possible, citations should provide pingback-like functionality (this may only be practical within OpenSAFELY-hosted study definitions).  It should be possible to see all variables authored (or contributed to) by a given user.  It should be possible to version and fork variables.

In some cases, a single concept may be covered by many competing interpretations. In these cases, the tool should make it easy to discover these similar definitions, and to assess them side-by-side, comparing their citations and clinical review history.

Variables often make most sense when combined with other variables. Sometimes a variable is composed of other variables; for example, a QRisk score requires BMI, sex, age, ethnicity, and so on.  In other cases, variables that are independent may still make sense to be usable as a group. For example, basic demographics (sex, age, region, IMD) almost always come together.  In some cases, an entire study definition might be a reusable component - for example, our vaccine eligibility study definition is an implementation of the "official" PRIMIS spec, so it would makes sense for anyone doing related research to be able to do the equivalent of `import primis_vaccine_eligibility_variables`.

For the time being, we're just documenting all the bits that comprise some common variables [in a Github issue tracker](https://github.com/opensafely/variable-library/issues) while we understand the problem more (see [this OFP](https://github.com/opensafely-core/roadmap/discussions/5)).


# 5: Actions library

An action is a unit of execution (implemented as a docker image) which takes data inputs and transforms them to predefined data, text, or graphical outputs.

Some examples include:

* A *cohort reporter*: takes the dataframe generated by any study definition and produces known-safe descriptive statistics about it: bar charts, maximums, minimums, %age null values, etc.  It's anticipated nearly all studies will start with this step as a means for checking assumptions about the real data. With the correct arguments, it may be that individual charts from this report could be prepared for direct use in academic papers, etc. [ticket](https://github.com/opensafely-core/cohort-extractor/issues/344)
* *Inclusion flowchart generator*: epidemioligical studies always start with a flowchart showing how the patient population was selected. This could be automated based on the study definition. [Ticket](https://github.com/opensafely-core/cohort-extractor/issues/167)
* A *anonymity metrics producer*: a script that provides a metric of a given dataframe's q-anonymity score ([ticket](https://github.com/opensafely-core/cohort-extractor/issues/126))
* *Measures charts*: easily-generated, OpenPrescribing-style prevalence-over-time charts, stratified and filtered ([repo we might base this on](https://github.com/opensafely/SRO-Measures))
* *Case matching*: finding matching cases in a patient cohort ([repo](https://github.com/opensafely/matching))
* *Safe cross-tabs*: automatically low-number-supressed crosstabs ([repo](https://github.com/opensafely-core/safetab-action), [OFP](https://github.com/opensafely-core/roadmap/discussions/4))
* *Canned data warnings*: look for known-odd patterns in data and report on them - excessive future dates, future dates for dead patients, unusually large numbers of nulls, etc

The library itself will take the form of documentation; using a item from a library will involve providing a line in a `project.yaml` (or, potentially, generating this from a UI).

We are [in the process of defining](https://github.com/opensafely-core/job-runner/issues/124) what our actions API looks like

# 6: Support OpenSAFELY self-service backends

Our vision is for OpenSAFELY to become the preferred platform for all kinds of research against many kinds of data. As a team, we have no desire to be a support and maintenance team for a platform; furthermore, we'd like the OpenSAFELY approach to evolve into something self-sustaining, to help ensure its future viability.

Currently, by way of requirements discovery, we are in discussions with third parties to install and develop proof-of-concept backends within their environments.

Ultimately, we should be in a position to give third parties documentatio for them to install and maintain a backend themselves.

This implies a number of things:

* Tooling to support the equivalent of `sudo install opensafely`; this may simply be via the provision of a pre-provisioned ubuntu VM, for example
* Supporting documentation on hardware requirements, configuration options, security considerations, monitoring considerations, etc
* Our job server would probably remain a single preferred point of coordination for any backend, but it should be possible for people to run and install their own job servers too.
* A plan, including timeline, for migrating our proof-of-concept installs to a self-managed production install. Otherwise we run the risk of maintaining legacy systems indefinitely
* Clear versioning, changelogs, and upgrade processes for all components in the platform

## Backend development



# 7: Peer support community

In line with our goals to help the OpenSAFELY project towards being relatively self-sustaining, we would like to encourage users to help each other out. This implies active community management by an individual with expertise in this area, and norms and tools around this. There are probably sub-communities (epi researchers; NHS operational analytics; platform developers; platform deployers).  Discussion forums remain a simple, common denominator. We may well want to support something like Slack communities. We will probably want to encourage conferences and other networking events.

We can count this goal as successful if at least 30% of support enquiries are resolved by users outside the Datalab team.

# 8: Privacy infrastructure

Our privacy claims are central to the OpenSAFELY vision.

We should have a public statement of our privacy design (based on [this draft](https://docs.google.com/document/d/1Ase87h_ogwjCjj3MOehBB2cduImQ-iWMiavmCiPiHrE/edit), perhaps?).

We should undertake regular adversarial testing of the platform and individual projects.

There should be at least one member of staff with time dedicated to regular
review of our privacy design and implementation.

One way of deciding we've achieved this goal is via some form of certification,
e.g. ISO27001, to assure that our processes are thorough and maintained.









