# TripRescue — Interview Guide & Technical Defense

## 1. Pitches
- **30-Second Pitch**: "TripRescue is a graph-based travel disruption recovery engine that models multi-leg journeys as a DAG, simulates cascading delay impacts across transit connections, and generates Pareto-optimal recovery plans ranked by cost, arrival time, and transfer risk."
- **2-Minute Pitch**: "When a flight is delayed, the impact ripples across connecting flights, train transfers, and hotel reservations. TripRescue models complex multi-leg itineraries as a Directed Acyclic Graph. When a disruption event occurs, our backend uses topological graph traversal to compute downstream buffer violations and identify broken connections. Our recovery engine searches multi-modal transportation alternatives (flights, trains, and layover reroutes) and uses Pareto-frontier multi-objective optimization to present ranked recovery packages balancing cost, delay, and connection risk with transparent visual explanations."

## 2. Key Technical Q&A
- **Q: Why model an itinerary as a DAG rather than a simple ordered list?**
  - **A**: Multi-passenger or multi-modal trips frequently fork and join. A DAG accurately models parallel temporal constraints and Minimum Connection Time (MCT) dependencies.
- **Q: How does Pareto ranking help travelers make better decisions?**
  - **A**: Rather than prescribing a single arbitrary metric, Pareto ranking filters out strictly inferior routes and presents clear trade-offs between speed, cost, and reliability.
