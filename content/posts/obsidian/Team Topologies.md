
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

## Team First Thinking

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
- 


