---
layout:     post
title:      "Clean architecture"
subtitle:   "来自大叔"
date:       2020-03-09 08:34:00
author:     "aguozhang"
header-img: "img/post-bg-2015.jpg"
tags:
    - architecture 
    - 大叔
    - 原则
    - 
---


### 前方
来自大叔的一本好书，内容浅显易懂。

大叔以自己的职业生涯为原材料，将看起来高大上的东西一一都讲明白了，并告诉应该怎么样去设计一个架构

### 摘录

* 所谓架构，就是你希望能在项目一开始就做对，但是却不一定能够做以的决策的集合。
* 其中一条比较黑暗的路线认为，只有威权和刚性才能带来强壮稳定的软件架构。如果某项变更成本太高，那么就忽视它--变量背后的需求要么被抑制，要么被丢到官僚主义的大机器中绞碎。架构师的决定是完整的、彻底极权的。软件架构就是全体开发人员的反乌托邦噩梦，永远是所有人沮丧的源泉。
* 软件架构是一个猜想，只有通过实际部署和测量才能证实。
* 走得快的唯一方法，是先走好
* 计算机代码没有变化 
* Get it works and get it rights is different
* it's a little utopian, but I have been to the promised land
* Architecture and design have no different, none at all. higer level also have low level details when you do design
* The goal of software architecture is to minimizie the human resources required to build and maintain the required system
* The story itself illustrues the foolishness of overconfidence
* Some butts of the developer does sleep -- the part that knows that good, clean, well-designed code matters
* Making messes is always slower than staying clean
* Their overconfidence will drive the redesign into the same mess as the original project
* avoid its own confidence
* software and hardware. 
* socpe and shape
* Therefore architectures should be as shape agnostic are practical
* Each of the paradigms removes capabilities from the programmer
* C have better encapsulation to C++
* Half point for inheritance
* The power of polymorphism
* Device independent
* Any source code dependency, no matter where it is, can be inverted
* By inserting an interface between them
* OO is the ability, through the use of polymorphism, to gain absolute control over every source code dependency in the system.
* Immutability from functional programming
* Event sourcing
* SOLID
* The code that implements high-level poliyc should not depend on the code that implements low-level details. Rather, details should depend on policies
* A module should be responsible to one, and only one, actor
* The word cohesive implies the SRP. Cohesion is the force that binds together the code responsible to a single actor.
* separate code that supports different actors
* OCP the open-closed principle
* A software artifact should be open for extension but closed for modification
* Interactor contains the business rule
* LSP the liskov substitution principle
* Pertains to interfaces and implementations
* ISP the interface segregation principle
* In general, it is harmful to depend on modules that contain more than you need 
* The lesson here is that depend on something that carries baggage that you don't need can cause you trouble that you didn't expect
* DIP The dependency inversion principle
* Source code dependencies refer only to abstractions, not to conretions
* Don't refer to volatile concrete classes
* Don't derive from volatile concrete classes
* Don't override concrete functions
* Never mention that name of anything concrete and volatile
* At least one such concrete component ofen called main because it contains the main function
* Component principles:
* Programs will grow to fill all available compile and link time
* The reuse/release equivalence principle
* The granule of reuse is the granule of release
* The common closure principle
* Gather into components those classes that change for the same reasons and at the same times. Separate into different components those classes that change at different times and for different reasons
* For most applications, maintainability is more important that resuability
* If the code in an application must change, you would rather that all of the changes occur in one component 
* A minimal number of components
* The common reuse principle
* Don't force users of a component to depend on things they don't need
* Don't depend on things you don't need
* The forces that impinge upon the architecture of a component structure are technical, political and volatile
* Allow no cycles in the component dependency graph
* ADP acyclic dependencies principle
* You must manage the dependency structure of the components
* DAG directed acyclic graph
* TOP Down design, the most important
* The stable dependencies principle: depend in the direction of stability
* One sure way to make a software component difficult to change, is to make lots of other software components depend on it.
* Stability: not easily moved 
* Not all components shoud be stable
* The stable abstraction principle: A component should be as abstract as it is stable
* Zone of pain
* Zone of uselessness
* The dependency management metrics described in the chapter measure the conformance of a design to a pattern of dependency and abstraction that I think is a good pattern 
* The architecture of a software system is the shape given to that system by those who build it
* The strategy behind that facilitations is to leave as many options open as possible, for as long as possible
* Deployment, maintenance and ongoing development
* Maintenance is the most costly
* Keep options open 
* The goal of the architect is to create a shape for the system that recognizes policy as the most essential element of the system while making the details irrelevant to that policy 
* Delayed and deferred
* A good architect maximizes the number of decisions not made
* Any organnization tht designs a system will produce a design whose structure is a copy of the organization's commnunication structure
* Welcome to the real world
* Then there is flase or accidental duplication 
* Source level, Deployment level, Service level
* Software architecture is the art of drawing lines that I call boundaries
* These are rendered ancillry and deferrable
* We didn't implement those methods t first
* I short, drawing the boundary line helped us delay and defer decisions, and it ultimately saved us an enormous amount of time and headaches. And that's what a good arhiteture should do
* The interface does not matter to the model -- the business rules
* Managing and building firewalls against this change is what boundaries are all about
* Software systems are statements of policy. Indeed, at its core, that's all a computer program actually is. A computer program is a detailed description of the policy by which inputs are transformed into outputs
* Level is the distance from the inputs and outputs
* If we are going to divide our application into business rules and plugins
* Critical Business Rules
* All that is required is that you bind the Critical Business Data and the Critical Business Ruels together in a single and separate software module
* A use case describes application-specific business rule as opposed the critical business rules within the Entities
* Use cases contain the rules that specify how and when the Critical Business Rules within the Entities are invoked. Use cases control the dance of the Entities
* Business rules are the reason a software system exists. the are the family jewels
* HOME
* Architecure are structures that support the use cases of the system
* Oh those are details that needn't concern us at the moment. We'll decide about them later
* Independent of framework
* Testable
* Independent of the UI
* INdependent of the database
* Independent of any external agency
* Source code dependencies must point only inward, toward higher-level policies
* The inner are policies
* Entities
* Use cases 
* Interface adapters
* Frameworks and drivers
* The important thing is that isolated, siple data structures are passed across the boundaries. We don't want to cheat and pass Entities objects or database row. We don't want the data structures to ahve any kind of dependency that vioaltes the Dependency rule
* The humble object pattern => Presenters and views
* The view is humble
* The separation of the behaviors into testable and dnon-testable parts often defines an architectural boundary
* Database gateways
* YAGNI
* Partial Boundaries
* Skip the last step
* One dimensional boundaries
* Facades
* Layers and boundaries
* Have to aware that such boundaries, when fully implemented, are expensive
* So what do we do, we architects? the answer is dissatisfying
* You must see the future. You must guess --intelligently
* It takes a watchful eye
* The main component is the ultimate detail-- the lowest-level policy, the dirtiest
* Think of main as a plugin to the application
* Services are partially true
* The Kitty problem
* All of them
* Services do not need to be little monoliths
* The tests are part of the system
* Fragile tests problem
* App-Titude Test
* First make it work
* Then make it right
* Then make it fast
* The target-hardware bottleneck
* The hardware is a detail
* The processor is a detail
* The operating system is a detail
* OSAL HAL
* The database is a detail
* They were absolutely right and I was wrong
* The web is a detail
* Frameworks are details
* Don't marry the framework
* It turns out that the devils is in the implementation details, and it's really easy to fall at the last hurdle if you don't give that some thought, too
* Package by layere
* Package by feature
* Ports and Adapters
* Package by component
* Components are the units of deployment. they are the smallest entities that can be deployed as part of a system. In java, they are jar files.

