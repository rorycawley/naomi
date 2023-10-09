# naomi

Functional onion architecture, with CQRS and Event Sourcing.

Dependencies between layers are created using project references. This allows dependencies to be explicit and in a single direction. Each layer is a separate project. This allows for any layer implementation to be replaced and it only affects the layer above.

In a 3 tiered architecture the business logic depends on the data access layer, so changing the data access layer impacts the business logic. Data access logic gets mixed with business logic.

We want a domain centric architecture not a database centric architecture.
(is each service a different solution?)

The relationships are, everything related down to the domain:
Presentation -> Application
Infrastructure -> Application
Infrastructure -> Database
Application -> Domain

The business logic in the domain is entirely independent from any infrastructure code.

We interact with interfaces, not caring about how it is implemented.

Create a gitignore file:
dotnet new gitignore

Create the projects:
dotnet new webapi -o GymManagement.Api
dotnet new classlib -o GymManagement.Application
dotnet new classlib -o GymManagement.Infrastructure
dotnet new classlib -o GymManagement.Domain

Create the references, which are the layer dependencies:
dotnet add GymManagement.Api reference GymManagement.Application
dotnet add GymManagement.Infrastructure reference GymManagement.Application
dotnet add GymManagement.Application reference GymManagement.Domain

Create the solution:
dotnet new sln --name "GymManagement"

Add the projects to the solution
dotnet sln add **/**.csproj

Build the solution:
dotnet build
