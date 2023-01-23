
---
title: Team Topologies
date: 2022-12-11 00:00:00
---
---

## Chapter 1 - Problem with org charts

Most IT organizations have a big challenge 
	of being fast (time to market), adaptable (pivot) and being safe (great experience for the user). 

To achive success most organizations split the work in business units, and use a "map" to clarify expectations (the **org-chart**)

This creates bottleneck's communications, but don't worry, great employes will find alternative communication paths. There are 3 types of communication path in any org:
	- Formal path: the org chart
	- Informal path: realm of the personal influence
	- Value creation structure: How work is actually gets done

in Team Topologies, we see the team as an indivisible block with explicit  expectations and interaction mode to work with other teams. With these ingredients expectations are clears and inter-trust team grows

### The Conway Law

> Organizations which designs systems... are constrained to produce designs which are copies of the communication structures of the organization

That means that you need to understand communications of your org, to realistically consider what kind of software architecture are feasible 

Example:
- If you have 4 teams building a compiler -> most likely you will have a 4 step compiler
- If your organization is divided in backend and frontends, you most likely  will have different 2 projects for each product.

**Inverse conway maneuver**: Where org setup teams to produce the architecture you want to produce -> forcing the communication channels by setting the teams

### Cognitive Load and Bottlenecks

**Cognitive Load**: Everybody has a limit of how much information they can hold in their brain. 

If we don't take into account **cognitive load**, teams will spread thin trying to cover an excess of responsabilities and domains. Having issues to pursue **mastery** and having a high cost of context switch

But often, we plan new products as if the team that is going to do them don;t have anything else to do -> raising the cognitive load -> lowering mastering -> probably lowering morale

## Chapter 2 - Conway Law 

> If the architecture of the system and the architecture of the organization are at odd, the arquitectures of the organization wins

In particular, an organization that is arranged in functional silos (where teams specialize in particular function, such as QA, DBA, or security) is unlikely to produce software systems that are well-architected for end-to-end flows.

So communication paths (formal or not) whitin an organization effectively restrict the kinds of solutions that the organization can device

That means we need to understand what software architecture is needed before we  organize our teams

> Team assigments are the first draft of the architecture

Meaning that if managers are deciding which teams built what... they are actually defining the final architecture

Good part of it, is we can use old fashion software architecture concepts to design our teams

- Loose coupling 
- High Cohesion
- Clear and appropiate cross-team testing 

### Restrict unnecessary communication

Many org assume that more communication is always better. But it's not the case

Communication is expensive and we should look closer to what kind of communication between teams we have. For fast flow we need to be aware of why we are communicating with other teams.

If we could achieve low-bandwidth communication between teams and still build and release fast and safe, then we should

If in the org, there is need to everybody approve something, or everybody to chip in into opinions, that would lead to monolithic architectures that are convoluted. Is better a cohesive view even if it's not your best ideal, that a mix and match between different visions.

## 3. Team First Thinking

**What is a team**: a stable group of 5 to 9 people who works toward a shared goal as a unit. A team has whole ownership of a value stream.

We consider the team to be the smallest entity of delivery


**Stable**: Meaning that people should not move really often (like maybe rotate each 9month to a year). But specially not having people that joins to help and go out after a month.

**Ownership**: helps to provide the vital continuity of care that moderns systems need. Also helps the team to thing  in horizons. 

**Two teams should not have ownership of the same system**, that way feedback is direct and there is a cohesive vision for the system.


### Dunbar Number 

There is a limit on our social skills as a human.

- around 5 people: limit of people with whom we can hold close personal relationship
- around 15 people: limit of people with whom we can experience deep trust
- around 50 people: limit of people with whon we can have mutual trust
- around 150 people: limit of people whose capabilities we can remember

teams around 5 to 9 -> which is the number on which we can have real high trust -> which is necessary for a team.

###  Tucjman Teal Perfomance model
1. **Forming**: assembling for the first time -> we still shy and correct
2. **Storming**: Working throught differences (personal and and professional) -> defining ways of working
3. **Norming**: Ways of workings start to be a standard and team mates starts to see them self as a unit.
4. **Performing**: Working as a unit.

This whole cycle could take around 3 weeks to 3 months. We should try to minimize the amount of time.

### Reward the whole team, not individuals
### Embrace diversity in teams
### Good boundaries minimize cognitive load

### Restrict team responsabilities to match team cognitive load

**Cognitive Load**: Total amount of mental effort being used in the working memory

- **Intrinsic cognitive load**: Intrinsic to the problem spaces
- **Extraneous cognitive load**: Relates to the environment (example -> how do I deploy this component again?)
- **Germane cognitive load**: relates to aspects that need special attention

Organizations should reduce to the minimum the *intrinsic*  (by trainings) and the *extraneos* (by making things easier).

Leaving more space for germane cognitive load, which is where the knowledge workers add value

If the stress of a team by the domain they are working is greater that the cognitive load of the team, the team will stop acting as a high performing units, and will start to act as as loosely associated group of individuals.

The team, also needs space to continuously reduce the cognitive load they are creating.

###  Match Software boundary size to team cognitive load

### Limit the number and type of domains per team

Types of domains:
- **Simple**: Most of the work has a clear path to action
- **Complicated**: Changes need to be analized and might need a few iterations to get it right
- **Complex**: Solutions require a lot of experimentation and discovery

Heuristics

1. If a domain is too big for a team, split the domain into subdomains and assign to the team
2. A single team can handle 2 or 3 **simple** domains. 
3. A team responsable for a **complex** domain, should not have any other domain
4. Avoid a single team, having 2 complicated domains, seems possible with big teams, but in reality the team will act a two (team mates will specialize into one or another domain)

### Match software boundary size to team cognitive load

Instead of choosing between monolith or microservice architecture. Design the software to fit the maximium team cognitive load. that will unblock safe, fast software delivery without extra costs.

How can we increase team cognitive load

- Have a good environment (physical or remote)
- Minimize team distractions
	- reduce meetings
	- assign a dedicated person to support queries and so forth
- Change the management style from "How" to What even Why
- Increase quality of developer experience
- Use a platform that is explicitly designed to reduce cognitive load for teams that build software on top of it


## Chapter 4. Static Team Topologies

To get most of our teams as possible, we need to consciously design our teams, instead of organic.

We should discourge team members o be shufled too much frequently. This leads to volatile teams assembled for projects, instead of team first approach that will build and mantain the projects.

### Shape team intercommunication to enable flow and sensing

Some organizations seem to assume that software delivery is one-way process, leading from specificiation to design, from design to coding, from coding to testin, from testing to releasing.

Instead, teams that are exposed to live environment tend to address user-visible and operational problems much more rapidly.

A team should have all the skills necessary, design, develop, test, deploy and operate. 

Such team (cross-functional) can bring high value to an organization by delivering cross-component, customer-centric features much faster than multiple "component" teams. But for this to work... they need to be able to deliver features into production without waiting for other teams.

### Product teams need a support system

The key to remain autonomous is to convert external dependencies to non-blocking. For example is extremly difficult to ensure a separate QA team will be available to evaluate a new feature exactly when the product team finishes

Non blocking dependencies, often take the form of self-service capabilities (example creating pipelines, onitoring tools) developed and mantained by other teams.

Without that, product teams end up frequently waiting on "hard dependencies" to functional teams (like QA, infrastructure etc..). This increase the friction as product teams are pressured to deliver faster.

### Cloud teams don't create application infrastructure

Since product teams, need this self-service approach, they cannot wait for a cloud team to provision in the infrastructure. On the other hands, Cloud teams are accountable for complience  and risk and can't let the product teams build provision whatever they want.

The solution: Cloud teams should provide a high-quality service that is able to provision the product-teams needs, with all the requirements, and product teams can only use this services.

So, the design of the cloud is done by the Cloud team, but the provision is done  by the product team.


## Chapter 5. The four fundamental Team topologies

### Steam-aligned teams

A stream is the continuous flow of work aligned to a business domain. This requires clarity of purpose and responsability so that multiple teams can coexist, each one with their own flow of work. This clarity helps to have a steady flow of work that the team can priotarize.



- Is the primary team type in an organizations
- The purpose of the other team types, is to reduce the burden of the stream-aligned teams
- Cause they work on the delivery, they are closer to the customer and able to quickly incorporate feedback while monitoring their software in production

Capabilities that all Stream aligned teams should have
- Application security
- Commercial and operational viability analysis
- Design and Architecture
- Development and Coding
- Infrastructure and operability 
- PRoduct management and ownership
- Testing and quality assurance
- User Experience

Each of this capabilities should not map to and individual role in the team

Team members should strive to achieve "autonomy, mastery and purpose"

### Enabling teams

Enable teams helps stream-aligned teams to use best-practices without the burden of having to investigate and experiment.

Comes enabling-teams to the rescue. 

The way enabling-teams works, is completly oposite to ivory towers, insteads of defining policies for all other teams, the idea is that they are in contact with all the teams, and when a team misses a capability they jump in, working hand by hand with the team.

This way stream-aligned teams have autonomy.

- They should listen to what stream-aligned teams need
- Should try to stay ahead of the curve before the need is expected from stream-aligned team
- Should acts as a messenger (new libraries, new bugs, this is unmantained better not use it anymore)
- Occasionally help if internal or external services are too hard to work with
- Promote learning in the whole organization (create communities)

If you got a "architect" teams, the most sensible thing would be to transform it into an full time enabling team, let's help the actual dev to upskill their abilities instead of making policies.

### Complicated-Subsystem Teams

All organizations have complicated systems, and we don't want to pollute all our tech landscape with the complexity of our ERP.

They know how the complicate systems work, and collaborate to build solutions together with the stream-aligned teams to create easier interfaces to use the system

### Platform Teams

The purpose of the platform team, is to enable stream-aligned teams to deliver work, with substantial autonomy. The stream-aligned team maintains full ownership of building, running and fixing the application in production.

The platform teams provide internal services to reduce the cognitive-load for the stream-aligned teams to deliver the code to the users.

Platform teams shoud have always in mind the "ease of use" of their internal services. They need to treat the services they offer as products, that are reliable, usable and fit for their purpose.

### Avoid team siles in the flow of Change

Generally speaking, teams composed only of people with a single functional expertise should be avoided if we want to deliver software rapidly and safely. Examples:

- Testing // QA
- Database administration
- UX
- Architecture

### A good platform is "Just Big Enough" // Thinnest viable platform

We don't need to go crazy creating a new platform, each thing we make we have to maintain and will be hard to replace and change.

Instead is more interesting to have good standards, templates and well-proven best practices that Dev team can use to innovate.

Specially with cloud, where we can outsource all this services, and what we need to do is to:

> Make it easier for developer to do the right thing in the right way


## Chapter 6. Choose team-first boundaries

We want to align teams to the flow of work, meaning for most of the work, we want to minimize the number of teams that need to be involved (coordinated). In this way we increase autonomy and also minimize the wait times.

Also to have high performance teams, autonomy and ownership is crucial, teams should own, nurture and improve systems under there umbrella. That means that finding the correct splits of systems to teams is a quite important decision.

To split the tech landscape of systems to team boundaries, we will talk about "Fracture Planes" (places were is most easy to split things)

### Fracture Place: Busines domain bounded context

Bounded contexts is one of the artifacts of applying DDD, it would give us different subsistems that have an internal model and a business reason to exists.

This are ideal ways to split the systems, cause you get clear business domain and therefore goals. 

And with that, you align the teams with the work of flow (most work of a bounded context not need to be coordinated with other bounded contexts)

### Fracture plane: Regulatory Compliance

In highly regulated industries, regulatory requirements set hard borders for software. They force organizations to adopt specific mechanisms for auditing, testing etc...

So maybe it makes sense that these systems have different deployments strategies (manual stepts etc...) that the rest of the system

### Fracture plane: Change Cadence

Spltting off the parts of the system that typically change at different speeds allow them to change more quickly.

### Fracture plane: Team Location

Use co-locations or true remote first approach

With covid, that lost most of the sense.

### Fracture plane: Risk

Different risk profiles might coexist withtin a large monolith. Taking more risk means accepting a higher propability of system or outcome failure in favor of getting changes into the hands of customers faster.

### Fracture plane: Performance Isolation

### Fracture plane: Technology
Technology is one of the typical ways to split teams, divide the team between frontends/backends.

This split normally introduce more constraints, and reduce the flow of work, cause now you have dependencies for almost each work item, and the teams are less autonomous.

### Fracture plane: User personas
Dependending on the solutions provided, maybe different user personas need a set of different features.

For example in tier price products, maybe a team could be focused on making the high end features that customers want to pay more for it (ie. security, data etc...) and another is doing basic features that will be used for more users.

## Chapter 7: Team interaction modes

One thing to be avoided is the need for all teams to communicate with all other teams to achieve their end.

So it's important to consider how each team interact with each other. We think there should be 3 types of team interactions.

- Collaboration: Working closely together with another team
- X-as-a-Service: Consuming/providing something with minimal collaboration
- Facilitating: Help another team to clear impediments.

### Collaboration
Collaboration interaction mode is suitable where a high deegree of adaptability or discovery is needed, particularly when expliring new technologies or techniques. That's because it avoids costly hand-off between teams.

Be aware that collaboration should not be a long-term way to interact between teams, it should be during a limited time where both teams get the results of the discoveries. 

Too much collaborations might be a sympthom of incorrect domain boundaries or incorrect mix of skills in a team.

### X-as-a-service

X-as-a-service is suited when there is no discovery going on, is clear what we need, and there is a team responsible for providing to the rest of the teams. 

Teams provides an artifact (library, platform etc...) that just works lowering the cognitive load of the teams using it and also making them more predictable.

There is great clarity on who own's what, and less context is needed between the teams.

The team that provides, should have a strong sense of responsability towards the solution they provide. They should treat it like a real product, making sure they are building what teams need, priotarize accordingly, making sure it works as intended all the team and the ease of use (Dev Ex)

### Facilitating

Suited on siturations where a team would benefit from the active help of another team facilitating/coaching some aspect of their work

The goal is to enable the teams to be more effective, learn more quickly etc...


## Chapter 8: Evolve team structures with organizational sensing

the configuration of teams need to  evolve, depending on the stage of the organization.

The normal way is that teams **collaborate** a lot at the beginning as they are doing **discovering**. But this puts a more cogniteve load to both teams (both teams needs to understand the other side) but it worth it for the reduce lag it brings to the discovery. 

X-as-a-service is better for when predictable delivery is more important than rapid discovery.

So it's usual that teams first start very close collaboration, and then they move to X-as-a-service interaction

Also close collaboration don't scale well across the organization, the aim should be to create well-defined platform that other teams can simply use.

### Triggers for Team topologies evolution

#### Software has grown too large for one team
- System is too large for the team cognitive load
- That means that changesi n specific part of the system are always done by the same team mates -> creating silos
- that cna actually create hard dependencies on people instead of teams, increasing the risk of any development

#### Delivery cadence is becoming slower
- Feels like changes take more time to get to the users
- Team is losing autonomy, possibly waiting for other teams to do some function (testing, platform etc...)


#### Multiple business services rely on a large set of underlying services


