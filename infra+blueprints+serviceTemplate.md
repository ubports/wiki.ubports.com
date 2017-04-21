This is a template for a Service Blueprint. It details the information required for a good (and actionable) blueprint. 

# Title: infra/blueprints/[serviceName]

## Service Summary
A brief description of what the service provides. Include major architectural points (large pieces of software needed) and what the service should achieve.

## Service Layers/Hierarchy
A textual or graphical description of the service layers. Include interfaces with other services.

## Service Dependencies
Internal and external dependencies required for perfect operation of the service. Internal dependencies are services that run on UBports infrastructure. External dependencies are anything else.

## Service Deployment Requirements
The hardware, network, and licensing requirements for this service.

## Service Implementation Requirements
How to set up the service, including any prerequisites that must be satisfied.

## Service Migration Requirements
How the service can be migrated to another server / system / network / etc. Include whether the service can be migrated live or if it will need to be bumped.

## Milestones & Timeline
An overview of important events in the service's implementation with target dates.