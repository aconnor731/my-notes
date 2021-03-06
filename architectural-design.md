
Perry and Wolf defines a software architecture as a set of architectural *elements* that have a particular *form*, explicated by a set of *rationale*.

Architectural elements include processing, data, and connecting elements.

Form is defined by the properties of the elements and the relationships among the elements-that is, the constraints on the elements.

The rationale provides the underlying basis for the architecture by capturing the motivation for the choice of architectural style, the choice of elements, and the form.

Rationale is replaced with architectural properties in this system.

Perry and Wolf model:
- *Processing elements*: those that perform transformations on data
- *Data elements*: those that contain the information that is used and transformed
- *Connecting elements*: the glue that holds the different pieces of the architecture together

#### 1.2.1 Components
**Component**: an abstract unit of software instructions and internal state that provides a transformation fo data via its interface.

Perry and Wolf's processing elements are defined as those components that supply the transformation on the data elements.

A component in our system is defined by its interface and the services it provides to other components, rather than by its implementation behind the interface.

#### 1.2.2 Connectors
**Connector**: an abstract mechanism that mediates communication, coordination, or cooperation among components.

Examples include shared representations, remote procedure calls, message-passing protocols, and data streams.

Connectors enable communication between components by transferring data elements from one interface to another without changing the data. The external behavioral abstraction captured by the architecture ignores those details.

In contrast, a component may, but not always will, transform data from the external perspective.

#### 1.2.3 Data
**Datum**: an element of information that is transferred from a component, or received by a component, via a connector.

Example not included as data is information that is permanently resident or hidden within a component.

Components can also generate data, as in the case of a software encapsulation of a clock or sensor.

### 1.3 Configuration
**Configuration**: the structure of architectural relationships among components, connectors, and data during a period of system run-time.

### 1.4 Properties
Properties are induced by the set of constraints within an architecture.

The goal of architectural design is to create an architecture with a set of architectural properties that form a superset of the system requirements.

### 1.5 Styles
**Architectural Style**: a coordinated set of architectural constraints that restricts the roles/features of architectural elements and the allowed relationships among those elements within any architecture that conforms to that style.

Styles are a mechanism for categorizing architectures and for defining their common characteristics.

Style does not refer to the personalization of the design process.

Since referring to a named set of constraints as a style makes it easier to communicate the characteristics of common constraints, we use architectureal styles as a method of abstraction, rather than as an indicator of personalized design.

### 1.6 Patterns and Pattern Languages
A design patter is defined as an important and recurring system construct.

A pattern language is a system of patterns organized in a structure that guides the patterns' application.

A primary benefit of patterns is that they can describe relatively complex protocols of interactions between objects as a single abstraction, thus including both constraints on behavior and specifics of the implementation.

### 1.7 Views
*An architectural viewpoint is often application-specific and varies widely based on the application domain...*

### 1.8 Related Work
The object-oriented programming community has taken the lead in producing catalogs of design patterns, as exemplified by the "Gang of Four" book and the essays edited by Coplien and Schmidt [33].

Software design patterns tend to be more problem-oriented than architectural styles.

## Chapter 2: Newtwork-based Application Architectures
### 2.1 Scope
This dissertation examines the highest level of abstraction in software architecture, where the interactions among components are capable of being realized in network communication.

#### 2.1.1 Network-based vs. Distributed
The primary distinction between network-based architectures and software architectures in general is that communication between components is restricted to message passing.

#### 2.1.2 Application Software vs. Networking Software
Applications represent the "business-aware" functionality of a system.

Application software architecture is an abstraction level of an overall system, in which the goals of a user action are representable as functional architectural properties.

### 2.2 Evaluating the Design of Application Architectures
One of the goals of this dissertation is to provide design guidance for the task of selecting or creating the most appropriate architecture for a given application domain, keeping in mind that an architecture is the realization of an architectural design and not the design itself.

### 2.3 Architectural Properties of Key Interest
#### 2.3.1 Performance
##### 2.3.1.1 Network Performance
*Throughput* is the rate at which information, including both application data and communication overhead, is transferred between components.

*Overhead* can be separated into initial setup overhead and per-interaction overhead, a distinction which is useful for identifying connectors that can share setup overhead across multiple interactions (*amortization*).

*Bandwidth* is a measure of the maximum available throughput over a given network link.

*Usable bandwidth* refers to that portion of bandwidth which is actually available to the application.

Styles impact network performance by their influence on the number of interactions per user action and the granularity of data elements.

##### 2.3.1.2 User-perceived Performance
*Latency* is the time period between initial stimulus and the first indication of a response.

*Completion* is the amount of time taken to complete an application action.

#### 2.3.2 Scalability
Scalability refers to the ability of the architecture to support large numbers of components, or interactions among components, within an active configuration.

#### 2.3.3 Simplicity
The primary means by which architectural styles induce simplicity is by applying the principle of separation of concerns to the allocation of functionality within components.

#### 2.3.4 Modifiability
Modifiability is about the ease with which a change can be made to an application architecture.

Modifiability can be further broken down into evolvability, extensibility, customizability, configurability, and reusability.

Because the components participating in a network-based application may be distributed across multiple organizational boundaries, the system must be prepared for gradual and fragmented change, where old and new implementations coexist, without preventing the new implementations from making use of their extended capabilities.

##### 2.3.4.1 Evolvability
Evolvability represents the degree to which a component implementation can be changed without negatively impacting other components.

##### 2.3.4.2 Extensibility
Extensibility is defined as the ability to add functionality to a system.

Dynamic extensibility implies that functionality can be added to a deployed system without impacting the rest of the system.

Extensibility is induced within an architectural style by reducing the coupling between components, as exemplified by event-based integration.

##### 2.3.4.3 Customizability
Customizability refers to the ability to temporarily specialize the behavior of an architectural element, such that it can then perform an unusual service.

A componnent is customizable if it can be extended by one client of that component's services without adversely impacting other clients of that component.

##### 2.3.4.4 Configurability
Configurability is related to both extensibility and reusability in that it refers to post-deployment modification of components, or configurations of components, such that they are capable of using a new service or data element type.

##### 2.3.4.5 Reusability
Reusability is a property of an application architecture if its components, connectors, or data elements can be reused, without modification, in other applications.

The primary mechanisms for inducing reusability within architectural styles is reduction of coupling (knowledge of identity) between components and constraining the generality of component interfaces.

#### 2.3.5 Visiblity
Visibility in this case refers to the ability of a component to monitor or mediate the interaction between two other components.

Visibility can enable improved performance via shared caching of interactions, scalability through layered services, reliability through reflective monitoring, and security by allowing the interactions to be inspected by mediators (e.g., network firewalls).

#### 2.3.7 Reliability
Reliability, within the perspective of application architectures, can be viewed as the degree to which an architecture is susceptible to failure at the system level in the presence of partial failures within components, connectors, or data.

## Chapter 3: Network-based Architectural Styles
### 3.1 Classification Methodology
The purpose of building software is not to create a specific topology of interactions or use a particular component type - it is to create a system that meets or exceeds the application needs.

The architectural styles chosen for a system's design must conform to those needs, not the other way around.

#### 3.1.2 Style-induced Architectural Properties
Since we do not intend to declare any single style as being universally desirable for all types of software, restricting the focus of our evaluation simply reduces the dimensions over which we need to evaluate.

### 3.2 Data-flow Styles
#### 3.2.1 Pipe and Filter (PF)
In a pipe and filter style, each component (filter) reads streams of data on its inputs and produces streams of data on its outputs, usually while applying a transformation to the input streams and processing them incrementally so that output begins before the input is completely consumed.

This style is also referred to as a one-way data flow network.

The constraint is that a filter must be completely independent of other filters (zero coupling): it must not share state, control thread, or identity with the other filters on its upstream and downstream interfaces.

#### 3.2.2 Uniform Pipe and Filter (UPF)
The uniform pipe and filter style adds the constraint that all filters must have the same interface.

The primary example of this style is found in the Unix operating system, where filter processes have an interface consisting of one input data stream of characters (stdin) and two output data streams of characters (stdout and stderr).

### 3.3 Replication Styles
#### 3.3.1 Replicated Repository (RR)
Systems based on the replicated repository style improve the accessibility of data and scalability of services by having more than one process provide the same service.

These decentralized servers interact to provide clients the illusion that there is just one, centralized service.

Distributed filesystems, such as XMS, and remote versioning systems, like CVS, are the primary examples.

#### Cache ($)
Cache is the replication of the result of an individual request such that it may be reused by later requests.

This form of replication is most often found in cases where the potential data set far exceeds the capacity of any one client, as in the WWW, or where complete access to the repository is unnecessary.

Caching provides slightly less improvement than the replicated repository style in terms of user-perceived performance, since more requests will miss the cache and only recently accessed data will be available for disconnected operation.

On the other hand, caching is much easier to implement, doesn't require as much processing and storage, and is more efficient because data is transmitted only when it is requested.

### 3.4 Hierarchical Styles
#### 3.4.1 Client-Server (CS)
A server component, offering a set of services, listens for requests upon those services.

A client component, desiring that a service be performed, sends a request to the server via a connector.

A server is usually anon-terminating process and often provides service to more than one client.

Separation of concerns is the principle behind the client-server constraints.

A proper separation of functionality should simplify the server component in order to improve scalability.

This simplification usually takes the form of moving all of the user interface functionality into the client component.

The separation also allows the two types of components to evolve independently, provided that the interface doesn't change.

#### 3.4.2 Layered System (LS) and Layered-Client-Server (LCS)
A layered system is organized hierarchically, each layer providing services to the layer above it and using services of the layer below it. 

Layered systems reduce coupling across multiple layers by hiding the inner layers from all except the adjacent outer layer, thus improving evolvability and reusability.

Examples include the processing of layered communication protocols, such as the TCP/IP and OSI protocol stacks, and hardware interface libraries.

Disadvantages: add overhead and latency to the processing of data, reducing user-perceived performance.

Layered-client-server adds proxy and gateway components to the client-server style.

A proxy acts as a shared server for one or more client components, taking requests and forwarding them, with possible translation, to server components.

A gateway component appears to be a normal server to clients or proxies that request its services, but is in face forwarding those requests, with possible translation, to its "inner-layer" servers.

These additional mediator components can be added in multiple layers to add features like load balancing and security checking to the system.

Architectures based on layered-client-server are referred to as two-tiered, three-tiered, or multi-tiered architectures in the information systems literature.

LCS is a solution to managing identity in a large scale distributed system, where complete knowledge of all servers would be prohibitively expensive.

Instead, servers are organized in layers such that rarely used services are handled by intermediaries rather than directly by each client.

#### 3.4.3 Client-Stateless-Server (CSS)
Each request from client to server must contain all of the information necessary to understand the request, and cannot take advantage of any stored context on the server. Session state is kept entirely on the client.

Visibility is improved because a monitoring system does not have to look beyond a single request datum in order to determine the full nature of the request.

Reliability is improved because it eases the task of recovering from partial failures.

Scalability is improved because not having to store state between requests allows the server component to quickly free resources and further simplifies implementation.

The disdvantage of client-stateless-server is that it may decrease network performance by increasing the repetitive data (per-interaction overhead) sent in a series of requests, since that data cannot be left on the server in a shared context.

#### 3.4.4 Client-Cache-Stateless-Server (C$SS)
A cache acts as a mediator between client and server in which the responses to prior requests can, if they are considered cacheable, be reused in response to later requests that equivalent and likely to result in a response identical to that in the cache if the request were to be forwarded to the server.

#### 3.4.5 Layered-Client-Cache-Stateless-Server (LC$SS)
This style derives from both the layered-client-server and client-cache-stateless-server through the addition and/or gateway components.

An example system that uses an LC$SS style is the Internet domain name system (DNS).

#### 3.4.6 Remote Session (RS)
The remote session style is a variant of client-server that attempts to minimize the complexity, or maximize the reuse, of the client components rather than the server component.

Application state is kept entirely on the server.

This style is typically used when it is desired to access a remote service using a generic client (e.g., TELNET) or via an interface that mimics a generic client (e.g., FTP).

Advantages:
- easier to centrally maintain the interface at the server
- improves efficiency if the interactions make use of extended session context on the server

Disadvantages:
- reduces scalability of the server, due to the stored application state
- reduces visibility of interactions, since a monitor would have to know the complete state of the server

#### 3.4.7 Remote Data Access (RDA)
The remote data access style is a variant of client-server that spreads the application state across both client and server.

Advantages:
- a large data set can be iteratively reduced on the server side without transmitting it across the network, improving efficiency
- visibility is improved by using a standard query language

Disadvantages:
- the client needs to understand the same database manipulation concepts as the server implementation (lacking simplicity) and storing application context on the server decreases scalability.
- reliability also suffers, since partial failure can leave the workspace in an unknown state

### 3.5 Mobile Code Styles
Mobile code styles use mobility in order to dynamically change the distance between the processing and source of data or destination of results.

#### 3.5.1 Virtual Machine (VM)
Underlying all of the mobile code styles is the notion of a virtual machine, or interpreter, style.

#### 3.5.2 Remote Evaluation (REV)
In the remote evaluation style, derived from the client-server and virtual machine styles, a client component has the know-how necessary to perform a service, but lacks the resources (CPU cycles, data source, etc.) required, which happen to be located at a remote site.

The remote evaluation style assumes that the provided code will be executed in a sheltered environment, such that it won't impact other clients of the same server aside from the resources being used.

#### 3.5.3 Code on Demand (COD)
In the code-on-demand style, a client component has access to a set of resources, but not the know-how on how to process them. It sends a request to a remote server for the code representing that know-how, receives that code, and executes it locally.

The advantages of code-on-demand include the ability to add features to a deployed client, which provides for improved extensibility and configurability, and better user-perceived performance and efficiency when the code can adapt its actions to the client's environment and interact with the user locally rather than through remote interactions.

Scalability of the server is improved, since it can off-load work to the client that would otherwise have consumed its resources.

#### 3.5.5 Mobile Agent (MA)
In the mobile agent style, an entire computational component is moved to a remote site, along with its state, the code it needs, and possibly some data required to perform the task.

An application can be in the midst of processing information at one location when it decides to move to another location, presumably in order to reduce the distance between it and the next set of data it wishes to process.

### 3.6 Peer-to-Peer Styles
