# TripRescue — Engineering Guide & Mastery Document

## 1. What Is TripRescue?
TripRescue is an **explainable travel disruption recovery and contingency planning engine**. When multi-leg itineraries experience flight delays, cancellations, missed connections, or transport strikes, TripRescue models the traveler's journey as a Directed Acyclic Graph (DAG), calculates cascading disruption propagation, and generates Pareto-optimal recovery alternatives ranked across price, delay, and secondary disruption risk.

## 2. Real-World Problem Solved
1. **Cascading Connection Failures**: A 45-minute delay on Leg 1 can cause a missed 3-hour international connection, invalidating subsequent hotel and train bookings.
2. **Opaque Airline Rebooking**: Standard airline automated rebooking offers rigid single-airline options that may strand travelers for 24+ hours.
3. **Single-Objective Bias**: Traditional tools optimize only for cheapest or earliest arrival, ignoring transfer risk and hotel cancellation deadlines.
4. **Lack of Explainability**: Travelers are given new tickets without understanding why specific routes were chosen or what alternatives existed.

## 3. High-Level Architecture
- **Frontend**: React 18, Vite, TypeScript, Tailwind CSS, Lucide Icons, interactive Graph view.
- **Backend API**: FastAPI (Python 3.12), Pydantic v2, NetworkX.
- **Core Algorithmic Engines**:
  - `graph_engine.py`: Itinerary DAG builder, minimum connection time (MCT) validator, and cascade delay simulator.
  - `recovery_engine.py`: Multi-modal alternative route generator (flights, high-speed rail, regional transit).
  - `ranking_engine.py`: Pareto frontier multi-objective optimization (Cost, Total Delay, Transfer Reliability).
  - `risk_ai.py`: Grounded disruption risk evaluator analyzing historical airport buffer reliability.
- **Data Layer**: In-memory graph representation + JSON persistence for simulated flight schedules and disruption events.

## 4. Algorithmic Complexity & Graph Formulations
- **Itinerary DAG**: Nodes represent arrival/departure events; directed edges represent travel segments and layover buffers.
- **Cascade Disruption Traversal**: Traversed in topological order in O(V + E) time.
- **Pareto-Optimal Frontier**: Evaluates recovery options in 3D objective space (min Cost, min Delay, max Reliability), pruning strictly dominated alternatives.

## 5. Security & Reliability
- Strict input validation on IATA airport codes, UTC timestamps, and flight numbers.
- Rate-limited mock external aviation data providers with graceful fallbacks.

## 6. Testing Strategy
- Automated unit test suite verifying topological sort ordering, cascade delay math, Pareto dominance pruning, and API route responses.
