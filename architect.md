# Architect

First : All in 1 files
Second: UI - Manager - API,DB
Third : Apply Clean Architect

## Levels

View: UI
Controller: Logic Handling for Use case / Adapter: Framework like redux
Usecase: Business Logic
Entities - Domain: Like DTO

### Layers

### Pros

- Possibility to change
- Expected Test
- Optimal Result

### Cons

- Requires intentional design / can be overkill for small apps
- Designing Clean Architect from the beginning is expensive and hard for ideas that need rapid development for the market
- Time consuming to develop

#### Not fit

- small apps / disposal app
- fixed requirements
-

### Dependency Rules

- Arrow always points in 1 direction
-

### Usecase vs Entites:

- Entities rarely change
-

# Design Pattern

# Storage Layer architect

usually 3 layer

1. CRUD class - strategy ( app schema )

2. DB layer - request priority ( read(concurrent) - write(serialize) ) - usecase

- config
- application
- query / define which query in which transaction

3. ultimate query (input -> output) adapter
   - create query
   - receive objet and gen query
