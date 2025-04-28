# Summary: Alexander Tobol's Talk on VK's Architecture

## 1. Problem Background
- **VK** = one of the largest social networks in Russia.
- **Scale**:
  - 100M+ users,
  - 3M requests/sec (peak),
  - Petabytes of data (photos, videos, messages).
- **Challenges**:
  - Heavy load: standard MySQL/PHP couldn’t handle growth,
  - High reliability: <52 minutes downtime per year,
  - Scalability: rapid feature rollout without degradation.

## 2. Requirements
- **Performance**: Latency ≤120 ms,
- **Reliability**: 99.94% uptime,
- **Flexibility**: integration of ML, CDN, cloud,
- **Time-to-Market**: deploy every 30 minutes.

## 3. System Evolution
- **Architecture journey**:
  - 2006: PHP + MySQL monolith,
  - 2009: Custom microservices (C++) replace MySQL,
  - 2011: Custom UDP-based RPC protocol,
  - 2015: Distributed computing, ML for smart feeds,
  - 2017: In-house global CDN,
  - 2020: Erasure coding for storage (saves 40% space).
- **Key metrics**:
  - SLA: 99.94%,
  - Storage: 600+ PB, 20k servers.

## 4. Architectural Components
- **Frontend**:
  - 10k PHP servers (compiled to C++ via KPHP).
- **Backend**:
  - Microservices in C++, Go, Java (800+ clusters),
  - Custom RPC protocol (TypeScript-like serialization).
- **Storage**:
  - Erasure coding for multimedia,
  - CDN: 100+ nodes worldwide.
- **Infrastructure**:
  - Monitoring: 200M metrics, ≤3s delay,
  - Deployment: 200+ deployments/day, 8M lines of code built in 1.5 min.

## 5. Engineering Approaches
- **PHP optimization**: KPHP speeds up code 7–10×,
- **Custom CDN**: Anycast + BGP for load balancing,
- **Distributed storage**: erasure coding replaces RAID,
- **Fast deployment**: automated tests, incremental builds.

## 6. Solution Optimality
- **Strengths**:
  - Scalability: 3M RPS,
  - Reliability: high uptime,
  - Flexibility: support for Web3, blockchain innovations.
- **Weaknesses**:
  - Complexity: custom solutions require high expertise,
  - Cost: 20k servers + 1.5k cloud servers.

## 7. Conclusion
- **VK's architecture** = a trade-off between performance, reliability, and development speed:
  - Evolution: monolith → microservices → cloud,
  - Innovations: custom RPC, CDN, distributed storage,
  - Future: experiments with Web3 and decentralized storage.

### Personal thoughts:
- Why not use **gRPC** or other standard solutions instead of custom RPC?
- How will VK overcome **cold start problems** when adopting Web3 tech?

### Open questions:
- How does VK **balance** between custom and open-source solutions?
- Wanted more insights on **DDoS protection** and **metrics analysis**.

### Key terms:
- **Erasure coding**: storage with redundancy for fault tolerance,
- **Anycast**: routing to nearest node,
- **KPHP**: PHP-to-C++ transpiler for speed.
