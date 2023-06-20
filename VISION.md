# API Improvement Proposals: Mission and Vision

## Mission

Help organizations build consistent, uniform remote application programming
interfaces and clients.

## Vision

API Improvement Proposals help producers of APIs delight their users with API
styleguide tooling, API best practices and validation tooling, and client
generators.

AIPs provide an ecosystem of extensible tooling and guidance that can bring
maturity to an existing API governance program or bootstrap a new one. In order
to facilitate this tooling ecosystem, AIPs provide guidance about
resource-oriented API design.

The AIPs can be categorized around layers of projects, with each higher layer
building on top of the lower layers.

### Layer 1: API style guide tooling

As an organization exposes multiple APIs to customers, the value of consistency
across those APIs increases. Consistency allows customers to leverage their
knowledge of existing APIs and apply them to others.

To help organizations manage their API style guide, we produce tooling that
enables publishing and validation of their chosen styles. This includes:

- A style guide template, which provides a structure to organize and version
  style guides.
- Style guide generators, producing websites that serve as a repository of
  knowledge for a style guide.
- Linting frameworks, used to verify that an API schema adheres to the style
  guide.
- Runtime validation frameworks, used to verify that an API’s behavior adheres
  to the style guide.

This layer is valuable for organizations with existing best practices that they
would like to represent in a well-organized, consistent manner, as well as
validated adherence.

### Layer 2: API design guidance

Although APIs expose a wide variety of features, there are broadly applicable
design principles and patterns that apply to any domain. These can span from
fundamental design choices (resource-oriented design, naming conventions) to
higher-order design patterns (singleton resource, jobs).

To help style guide authors who would like to build their guide on best
practices, we provide a curated list of API design guidance, with clear
rationale attached to help a reader understand why the guidance is considered a
best practice.

This includes:

- Concise API guidance, allowing consumers to easily understand
  recommendations.
- Explanations of the design guidance, to help consumers understand why the
  choice was made.
- Granular linting and runtime validation rules, allowing organizations to
  validate adherence of guidance they choose to incorporate in their own style
  guide.

This layer is helpful for organizations who have some existing practices that
they would like to continue to incorporate, but would like to be inspired from
best practices.

### Layer 3: API Standard, Clients and Documentation

Aggregating all of the design guidance, we can provide an API standard,
characterized by strict adherence to all of the guidance rather than flexible
rules to pick and choose.

For organizations that choose to adhere to the API standard, we provide
generators that create high-quality clients, including:

- Command Line Interfaces.
- Documentation.
- SDK generation.
- Infrastructure as Code SDKs.
- Web User Interfaces.

This layer is valuable for organizations who would like strongly opinionated
best practices, and would like to reduce maintenance cost for bespoke clients.
