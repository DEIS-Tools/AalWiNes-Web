The AalWiNes network verification suite performs fast (polynomial time) verification of forwarding rules
in MPLS routing tables in the presence of link failures. In MPLS, packet labels can be nested 
in order to provide tunneling through the network or to handle link
failures by fast-reroute mechanism. This mechanism relies on pushing a new MPLS
label on top of the label stack, to redirect the flow 
to go around the failed link. This mechanism can be applied several times
in case of multiple link failures, creating larger and larger (in theory: unbounded)
numbers of MPLS labels on the label-stack.
The tool allows to verify a
wide range of important network properties in polynomial time,
parameterized by the maximum number of assumed link failures. 
At the core of the tool lies an expressive query language for reachability
analysis, based on regular expressions, both to specify packet headers as well
as constraints on the routes. Specifically, queries are of the form:

< a >   b   < c >   k

where a and c are regular expressions over MPLS labels that describe the 
set of allowed initial resp. final headers of packets in the
trace, b is a regular expression over the links in the network, defining the set
of allowed routing traces through the network, and k is a number
specifying the maximum number of failed links to be accounted for. 
By using regular expressions, the tool can
test properties such as waypoint enforcement (e.g., is the
traffic always forwarded through an intrusion detection system)
or avoidance of certain routers in selected countries. 
The tool also allows to account for more complex
traffic engineering aspects, such as load-balancing, by supporting
nondeterminism, as well as more complex multi-operation chains.

## How does polynomial-time what-if analysis work?

The model checking algorihtm relies on an automata-theoretic approach
and leverages a connection to the theory of pushdown automata.
In a nutshell, given the network configuration, the routing tables,
as well as the query, the tool constructs a pushdown automaton
(PDA). This PDA is then an input for the backend engine
that is used for reachability analysis. 
The tool also provides a witness trace generation
so that it can generate (among a possibly infinite number of witness traces)
the ones that minimize certain criteria (e.g. the number of hops, latency,
and the stack height that corresponds to the number of tunnels). This is
achieved by extending the PDA reachability analysis with multi-dimensional weights.
Despite the added complexity, the verification can be still performed in polynomial time.

## Graphical User Interface

Our tool allows to load an arbitrary network
topology (e.g., from the topology zoo dataset) as well
as a set of router configurations (e.g., from Juniper routers) into a GUI that
can be run in a browser.
The configurations are then put into an standardized, intermediate
format which is vendor independent. The user can then define
a query (see above), which leads the tool to prompt with a result
(e.g. a trace). 

![Screenshot of the GUI](img/screenshot.png =400x)
