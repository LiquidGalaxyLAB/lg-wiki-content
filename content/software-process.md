---
title: Software Process
contributor: Peter Atef
date: June 12, 2024
---

  
_**Introduction**_  
  
The **software process** is a structured set of activities required to develop a software system.  
  
There are many different types of software processes but all involve:  
1 - Specification: defining what the system should do.  
2 - Design and implementation: defining the organization of the system and implementing the system.  
3 - Validation: checking that it does what the customer wants.  
4 - Evolution: changing the system in response to changing customer needs.  
  
A **software process model** is an abstract representation of a process. It presents a description of a process from some particular perspective.  
  

* * *

  
_**Plan-driven and agile processes**_  
  
We will talk about two common software processes:  
**Plan-driven processes** are processes where all of the process activities are planned in advance and progress is measured against this plan. On the other hand, in **Agile processes**, planning is incremental and it’s easier to change the process to reflect changing customer requirements.  
In practice, most practical processes include elements of both plan-driven and agile approaches because there isn’t such thing as called right and wrong software process.  
  

* * *

  
_**The waterfall model**_  
It’s a software process model representing the plan-driven software process. It uses the following approach:  
  
![The waterfall model](https://lh7-us.googleusercontent.com/docsz/AD_4nXcV6PcaP1H7yp2Q0Ipztu1mziTtp2u5sFqRRPUQ3DM2DyMWu8q6NlVpeshErQcbzg1QEO1EVpOxCqb7W3TEd1xScS6fywykqsfAdR2y8JLUw1Zo17rVKA-jZooitOI2DNwQ6tefuVFS3hptd6wbOJ4C1Rr2?key=eXYxpY5rbSPIPtG3SWVZIQ "The waterfall model")  
There are separate identified phases in the waterfall mode:  
→ Requirements analysis and definition.  
→ System and software design.  
→ Implementation and unit testing.  
→ Integration and system testing.  
→ Operation and maintenance.  
  
As you can see from the diagram, it’s a sequential approach where we move to the next stage after finishing the current state completely. That will lead to a problem in case of customer modifications, assume the software team is working on the “implementation and unit testing” stage and the customer asks for a change in the main requirements of the project that will force the team to start the pipeline all over the again from the “Requirements definition” stage. So, the main drawback of the waterfall model is the difficulty of accomplishing change after the process is underway. In principle, a phase has to be completed before moving on to the next phase.  
  

* * *

  
_**Waterfall model problems**_  
  
_1 - Inflexible partitioning of the project into distinct phases makes it difficult to respond to changing customer requirements._  
→ Therefore, this model is only appropriate when the requirements are well defined and changes will be fairly limited during the design process.  
→ Few business systems have stable requirements.  
  
_2 - The waterfall model is mostly used for large systems engineering projects where a system is developed at several sites._  
→ In those circumstances, the plan-driven nature of the waterfall model helps coordinate the work.  
  

* * *

  
_**Process Activities**_  
  
Real software processes are inter-leaved sequences of technical, collaborative, and managerial activities with the overall goal of specifying, designing, implementing, and testing a software system. The four basic process activities of specification, development, validation, and evaluation are organized differently in different development processes. For example, in the waterfall model. They are organized in sequence, whereas in the incremental model (Agile) they are interleaved.  
  
**Software specification:** The process of establishing what services are required and the constraints on the system’s operation and development.  
  
Types of requirements in an engineering process:  
  
_1 - Requirements elicitation and analysis_  
→ What do the system stakeholders require or expect from the system?  
_2 - Requirements specification_  
→ Defining the requirements in detail  
_3 - Requirements validation_  
→ Checking the validity of the requirements.  
  
## Software design and implementation:
1 - It’s the process of converting the system specification into an executable system.  
2 - Software design is to design of a software structure that realizes the specifications.  
3 - Implementation: Translate this structure into an executable program.  
4 - The activities of design and implementation are closely related and may be inter-leaved.  
  
## Design activities
1 - Architectural design: where you identify the overall structure of the system, the principal components (modules), their relationships, and how they are distributed.  
2 - Database design: where you design the system data structure and how they are to be represented in the database.  
3 - Interface design: where you define the interfaces between the components.  
4 - Component selection and design: where you search for reusable components to speed up the implementation process. If unavailable, you design how it will operate.  
  
![Design activities](https://lh7-us.googleusercontent.com/docsz/AD_4nXcq2lqcTuKjqk-100zR1ivGY6njaCVnPvh2eZeU-tMmYhSrFl39Wp3DCaQrwo0425C9o0GVuUrnekjmjlJ1akZLKkuhlDBP0dEjJfnu3N9c8KBe1WHI8EZMv31TA4-qKRstIBTJw_F-4AyMG4LNoR4nKssh?key=eXYxpY5rbSPIPtG3SWVZIQ "Design activities")  
## System implementation
1 - The software is implemented either by developing a program or by configuring an application system.  
2 - Design and implementation are interleaved activities for most types of software systems.  
3 - Programming is an individual activity with no standard process.  
4 - Debugging is the activity of finding program faults and correcting these faults.  
  
## Software validation
_1 - Verification and validation (V & V) is intended to show that a system conforms to its specification and meets the requirements of the system customer._  
→ Verification is to make sure that my system meets the expected output "specifications" created in the first phase.  
→ Validation is to make sure that my system meets the customer's requirements because the specifications “expected output” may differ from the customer's requirements due to misunderstanding.  
_2 - Involves checking and reviewing processes and system testing._  
_3 - System testing involves executing the system with test cases that are derived from specifications of the real data to be processed by the system._  
  
![Software validation](https://lh7-us.googleusercontent.com/docsz/AD_4nXciro76xUBMpvttG1i3aCoeZ9GUDjguwHlV3dKMzvQMGuB3mRhMia58nCWqCnncNUj7XK18UaolofYKy-6vK9iFcguAACbsWPeBoshs3y3VH7E4qQKnKyCs3Qi3qaz6GZPVeRvEkxvvADagmvzx2hA_g5DG?key=eXYxpY5rbSPIPtG3SWVZIQ "Software validation")  
## Testing stages
_1 - Component testing_  
a - Individual components are tested independently.  
b - Components may be functions or objects or coherent groupings of these entities.  
_2 - System testing_  
a - Testing of the system as a whole. Testing of emergent properties is particularly important.  
_3 - Customer testing_  
a - Testing with the customer data to check that the system meets the customer’s needs.  
  
![Testing stages](https://lh7-us.googleusercontent.com/docsz/AD_4nXddj-znwDhdZEMyUYpXaVBE6PttdE5Ywf8ejin4-sFgOr9HmdVU92PHT3g2nb1_cXcgRBRVfm9_2pfato6c13dxPTLxqJZa6myhSL0H2PTyE9HZQAXK0gQxZGWq_9HUEHPoU0eYv507Mliv_ZwD3Bqp6UVq?key=eXYxpY5rbSPIPtG3SWVZIQ "Testing stages")  
## Software evolution
→ Software is inherently flexible and can change.  
→ As requirements change through changing business circumstances, the software that supports the business must also evolve and change.  
→ Although there has been a demarcation between development and evolution (maintenance) this is increasingly irrelevant as fewer and fewer systems are completely new.  
  
![Software evolution](https://lh7-us.googleusercontent.com/docsz/AD_4nXd6aXKPbkolC-OT25tSh0es-mX_ewDXMZs3eatp46akutPdJ_I32Yv_tpzkoALGPfb6WBOnAN7tnxkgElx1cJruTe5fMt4NCjIofEQQVlwgkC9ZO05MA7myrJGSuE8fRzcrVvGLS30vzbsArWFreFEA6vQ?key=eXYxpY5rbSPIPtG3SWVZIQ "Software evolution")  

* * *

  
## References
1 - Software Engineering 10th edition by Ian Sommerville  
a - Chapter 2: Software Process  
b - Chapter 3: Agile Software Development
