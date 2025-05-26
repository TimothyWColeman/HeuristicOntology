# HeuristicOntology
https://www.heuristicontology.com/

The Heuristic Ontology provides a formal semantic framework for representing heuristics as directive information content entities –structured, named, and computationally actionable constructs.

Unlike informal notions of heuristics as vague or unconscious tendencies, this ontology treats them as clearly defined, actionable specifications that can be named, classified, and linked to behavior within information systems. 

Heuristics are treated not as vague psychological tendencies, but as clearly defined, prescriptive specifications that can be operationalized by intelligent agents to guide decision-making. By aligning with Basic Formal Ontology (BFO 2020) and the Common Core Ontologies (CCO 2.0), this ontology ensures conceptual rigor, interoperability, and formal clarity across domains. It supports the classification, inference, and modeling of cognitive strategies in both human and artificial decision systems.

![image](https://github.com/user-attachments/assets/35ee9eda-7270-4c59-b5f0-8700e682ccaf)


# Heuristic Ontology (Version 2025-05-26)

The Heuristic Ontology provides a formal semantic framework for representing heuristics as directive information content entities - structured, named, and computationally actionable constructs. Unlike informal conceptions of heuristics as vague or unconscious tendencies, this ontology treats them as clearly defined, prescriptive specifications that can be operationalized by intelligent agents to guide decision-making. Heuristics are understood not as psychological traits but as modular information structures that direct behavior in the face of uncertainty, limited information, or time constraints. Grounded in Basic Formal Ontology (BFO 2020) and aligned with the Common Core Ontologies (CCO 2.0), this ontology ensures conceptual clarity, formal rigor, and interoperability across knowledge systems and application domains, with a focus on medical triage scenarios.

## Overview

The Heuristic Ontology models cognitive heuristics as Directive Information Content Entities (DICE), enabling formal representation of decision-making under constraints such as time pressure, incomplete data, or limited computational capacity. It organizes heuristics into four cognitive families—Decision Simplification, Exploratory, Social, and Temporal—each with specific subclasses (e.g., Availability Heuristic, Social Proof Heuristic). This version enhances support for medical triage applications, adding new properties, classes, instances, and reasoning constraints to model scenarios like the Simple Triage and Rapid Treatment (START) protocol.

Developed by researchers at SUNY University at Buffalo and the National Center for Ontological Research, and the ontology bridges cognitive science, behavioral economics, and applied AI. It supports use cases in medical triage, cognitive modeling, decision-support systems, and knowledge graph integration.

## Version Information

- **Version IRI**: http://www.heuristicontology.com/2025-05-26/HeuristicOntology
- **Release Date**: May 26, 2025
- **Changes in This Version**:
  - **New Object Properties**: `guided_by`, `guides_behavior`, `has_intended_outcome`, `is_applied_to`, `has_participant`, `has_input`, `has_output` to link heuristics to processes and outcomes.
  - **New Data Properties**: `confidenceLevel`, `cognitiveLoad`, `responseTime`, `expectedAccuracy`, `learningCurve`, `applicabilityScore` to quantify heuristic performance.
  - **Medical Triage Classes**: `MedicalTriageHeuristic`, `STARTTriageHeuristic`, `MedicalTriageDecisionProcess` for triage-specific modeling.
  - **Instances**: Added instances for triage scenarios, such as a medic using the Availability Heuristic (based on Exemplar 3 from Coleman et al., 2025).
  - **Reasoning Enhancements**: Introduced cardinality axioms (e.g., every `HeuristicGuidedProcess` requires a `guided_by` relation) and SHACL constraints for `MedicalTriageDecisionProcess`.
  - **Bug Fix**: Corrected syntax error in `AvailabilityHeuristic` restriction (changed to `BFO_0000056`).
- **Previous Version**: http://www.heuristicontology.com/2025-05-12/HeuristicOntology

## Installation and Usage

### Requirements

- **Protégé**: Version 5.5 or later for ontology editing.
- **OWL Reasoner**: HermiT or Pellet for consistency checking.
- **RDF Libraries**: Apache Jena or RDFLib for programmatic access.
- **SHACL Validator**: TopBraid SHACL API or similar for constraint validation.

### Loading the Ontology

1. Download `HeuristicOntology - 2025-05-26-Complete.ttl` from the Releases page.
2. Open in Protégé via `File → Open`, ensuring Turtle format is selected.
3. Run a reasoner (e.g., HermiT) to verify consistency.
4. Validate instances against SHACL constraints using a SHACL validator.

### Example SPARQL Query

Retrieve all medical triage decisions and their guiding heuristics:

```sparql
PREFIX : <http://www.heuristicontology.com/HO0000000272/>
SELECT ?decision ?heuristic ?output
WHERE {
    ?decision a :MedicalTriageDecisionProcess ;
              :guided_by ?heuristic ;
              :has_output ?output .
}
```

### Programmatic Access

Parse the ontology using RDFLib in Python:

```python
from rdflib import Graph
g = Graph()
g.parse("HeuristicOntology - 2025-05-26-Complete.ttl", format="turtle")
print("Ontology loaded successfully.")
```

## Dependencies

The ontology imports the following:

- **Basic Formal Ontology (BFO 2020)**: http://purl.obolibrary.org/obo/bfo/2020/bfo-core.owl
- **Common Core Ontologies (CCO 2.0)**:
  - AgentOntology: https://www.commoncoreontologies.org/2024-11-05/AgentOntology
  - CommonCoreOntologiesMerged: https://www.commoncoreontologies.org/2024-11-06/CommonCoreOntologiesMerged
  - ExtendedRelationOntology: https://www.commoncoreontologies.org/2024-11-06/ExtendedRelationOntology
  - GeospatialOntology: https://www.commoncoreontologies.org/2024-11-06/GeospatialOntology
  - InformationEntityOntology: https://www.commoncoreontologies.org/2024-11-06/InformationEntityOntology
  - TimeOntology: https://www.commoncoreontologies.org/2024-11-06/TimeOntology

Ensure these ontologies are accessible (e.g., via internet or local copies) when loading the Heuristic Ontology.

## Use Cases

- **Medical Triage**: Model heuristic-guided decisions in mass-casualty scenarios, such as applying the START protocol or detecting biases like the Availability Heuristic. For example, the ontology can represent a medic prioritizing a patient based on recalled similar cases.
- **Cognitive Science**: Analyze bounded rationality and heuristic strategies in decision-making under uncertainty, supporting research in behavioral economics and psychology.
- **AI Systems**: Integrate heuristics into decision-support systems, cognitive architectures, or explainable AI frameworks to enhance human-aligned decision-making.
- **Knowledge Graphs**: Link heuristic-guided processes to clinical data for auditing triage decisions or integrating with electronic health records.

## Example: Triage Scenario

The following instance models a medic using the Availability Heuristic to prioritize a patient (from Exemplar 3, Coleman et al., 2025):

```turtle
:AvailabilityHeuristicDecision123 rdf:type :AvailabilityBasedDecisionProcess , :MedicalTriageDecisionProcess ;
    :guided_by :AvailabilityHeuristic03 ;
    :has_input :PreviousSimilarPatientCase456 ;
    :has_participant :MedicResponder456 ;
    :has_participant :Patient123 ;
    :has_output :HighPriorityTriageAssignment789 ;
    :responseTime "PT5S"^^xsd:duration ;
    :cognitiveLoad "3"^^xsd:integer .
```

## Directory Structure

```
heuristic-ontology/
├── HeuristicOntology - 2025-05-26-Complete.ttl
├── README.md
├── LICENSE
├── CHANGELOG.md
├── CONTRIBUTING.md
├── docs/
│   ├── examples.md
│   ├── usage-guide.md
├── examples/
│   ├── triage-scenario-1.ttl
│   ├── sparql-queries.rq
├── scripts/
│   ├── validate.py
│   ├── query.py
└── .gitignore
```

## Contributing

We welcome contributions to refine the heuristic typology, add domain-specific heuristics (e.g., clinical diagnostics), or enhance reasoning capabilities. To contribute:

1. Fork the repository.
2. Create a branch (`git checkout -b feature/new-heuristic`).
3. Commit changes (`git commit -m "Added ClinicalDiagnosticHeuristic class"`).
4. Submit a pull request with a clear description and rationale.
5. Ensure changes align with BFO 2020 and CCO 2.0 standards.
6. Validate changes with Protégé and a SHACL validator.

Report issues (e.g., syntax errors, missing classes) via the Issues tab.

See CONTRIBUTING.md for detailed guidelines.

## License

This ontology is licensed under the Creative Commons Attribution 4.0 International License (CC BY 4.0). See LICENSE for details.

## Contact and Credits

- **Contributors**:
  - Timothy W. Coleman (timothywcoleman@gmail.com)
  - John H Bittner II (john.h.bittner@gmail.com)
- **Affiliations**: SUNY University at Buffalo, National Center for Ontological Research
- **Reference**: Coleman, T. W., Smith, B., Beverley, J., & Bittner, J. H. (2025). *Formalizing Heuristics: Cognitive Strategies for Decisions Under Constraint*.
- **Contact**: Open an issue or email the contributors for inquiries.
- **Issue Tracker**: https://github.com/yourusername/heuristic-ontology/issues

## FAIR Principles

The Heuristic Ontology adheres to FAIR (Findable, Accessible, Interoperable, Reusable) principles:

- **Findable**: Uses a persistent IRI and is documented for discovery.
- **Accessible**: Freely available on GitHub under CC BY 4.0.
- **Interoperable**: Aligned with BFO 2020 and CCO 2.0, using Turtle format.
- **Reusable**: Includes examples, scripts, and clear documentation.

## Acknowledgments

This work builds on foundational research in cognitive science and ontology engineering, with gratitude to the BFO and CCO communities for their standards and support.
