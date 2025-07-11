# 🧠 Agentic Self-Discovering Robotic Learning System

## 📄 Abstract
This document proposes a novel agentic architecture for robotic learning. Instead of relying on pre-defined, human-labeled motion primitives, the system autonomously discovers its own low-level primitives, iteratively chains them into more complex behaviors, and evaluates success or failure using internal feedback agents. Once successful "skills" are discovered, humans provide natural language labels, which are further expanded and interpreted by a language model (LLM) agent. This framework allows robots to generalize across different hardware configurations and to flexibly interpret human commands in natural language.

## 💡 Motivation
Robotic learning today often relies on human-defined primitives and large labeled datasets. These approaches limit flexibility and adaptability across different robot types ("species"). We aim to create a system where robots:
- Discover their own capabilities without human-defined motions.
- Learn to compose these capabilities into increasingly complex skills.
- Assign meaning and human language labels only after skills are proven useful.

## ⚙️ Core Principles
- **Primitive Discovery:** Robots autonomously explore their actuator space to identify feasible, distinct atomic movements (primitives).
- **Chaining and Skill Formation:** These primitives are combined into longer motion sequences to achieve complex tasks.
- **Evaluation Loop:** Agents continuously assess success or failure, providing feedback for retries or further exploration.
- **Human-in-the-Loop Labeling:** After successful skill discovery, humans assign natural language labels.
- **Language Model Agent Integration:** An LLM agent expands human descriptions into multiple phrasings, enabling robust natural language command interpretation.

## 🏗️ Architecture Overview

### 🟢 Mobility Constraints & Discovery Agent
- Explores actuator and kinematic space.
- Identifies and stores unique primitives based on end states.
- Starts with random or systematic small adjustments to avoid bias.

### 🟠 Chaining Agent
- Sequentially combines primitives to form chains.
- Increases chain length progressively as simpler chains succeed.

### 🔵 Success/Error Evaluation Agent
- Compares final state to goals or environmental changes.
- Classifies attempts as success, partial success, or failure.

### 🟣 Adjust and Retry Agent
- Modifies failed chains (e.g., changes last primitive).
- Avoids repeating identical failed paths.

### 🟤 Looper Agent
- Governs retry logic, exploration depth, and exit conditions.
- Decides when to abandon a path or move to longer chains.

### ⚪ Mirror Memory Agent
- Stores ideal or reference motions (optional human demonstrations or desired end states).
- Allows replaying or benchmarking attempts against "ideal" motions.

### ⚫ Long-Term Memory Agent
- Stores successful motion sequences (skills) along with context (e.g., robot config, object positions).
- Associates skills with human semantic labels.

### 🟡 Recall and Language Interpretation Agent
- Uses LLM to expand human-provided labels.
- Maps diverse human commands to corresponding stored skills.
- Suggests or auto-selects skills based on semantic similarity.

## 🔄 Learning Process Flow
1. **Primitive Discovery:** The Mobility Agent explores individual actuator capabilities, saving distinct movements.
2. **Initial Chaining:** Begin combining two primitives; increase chain length after successes.
3. **Evaluation:** Success/Error Agent assesses outcome; Adjust and Retry Agent refines failed sequences.
4. **Skill Formation:** Successful chains are promoted to skills and stored.
5. **Human Labeling:** Prompt human to describe each new skill; label is stored.
6. **Language Expansion:** LLM generates synonyms and alternative commands for each skill.
7. **Future Recall:** When given a new natural language command, the system matches to known skills and executes.

## 🚀 Advantages
- Hardware-agnostic: Works across different robot forms since primitives are self-discovered.
- Incremental learning: Systematically builds from simple motions to complex behaviors.
- Human-aligned: Language labels added after skills are proven, making human interaction intuitive and scalable.
- Modular and interpretable: Each agent can be refined independently, supporting future improvements or specialized extensions.

## 💬 Future Work
- Physical robot validation beyond simulation.
- Integration with vision-based goal recognition and dynamic scene understanding.
- Multi-robot skill sharing via decentralized or federated memory.
- Public open-source framework release with community contribution guidelines.

## 📅 Roadmap Milestones
1️⃣ Primitive discovery in simulation (e.g., Gazebo or Isaac Sim).  
2️⃣ Chaining and success evaluation loop working virtually.  
3️⃣ Basic long-term memory implementation and YAML/JSON skill storage.  
4️⃣ Human labeling interface (CLI or minimal web UI).  
5️⃣ LLM agent integration for label expansion and fuzzy matching.  
6️⃣ Public release of codebase and architecture documentation.

## 💥 Conclusion
This framework introduces a fundamentally new way for robots to learn: self-exploring, self-composing, and only after achieving success, integrating human semantics. By decoupling primitive discovery from human pre-labeling and modularizing feedback and memory agents, robots can achieve greater autonomy and adaptability. This document serves as both a vision statement and a working foundation to guide an open-source prototype and future research.

---

## 📄 System Architecture Diagram

[Mobility Discovery Agent] ──> [Chaining Agent] ──> [Success/Error Agent] ──> [Adjust & Retry Agent]
          │                                 │                       │                      │
          ▼                                 │                       │                      │
  [Primitive Store]                         │                       │                      │
          │                                 ▼                       │                      │
          └────────────> [Long-Term Memory Agent] <───┬─────────────┘                      │
                                                   │                                     │
                              [Mirror Memory Agent]                                     │
                                                   │                                     │
                           [Human Label Input] ───> [LLM Agent] ───> [Recall Agent] <───┘

---

**License:** No license is offered at this time; all rights reserved.  
**Author:** Xander Phoenix
**Date:** July 11, 2025
