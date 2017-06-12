---
layout: post
category : requirements
tagline: "Supporting tagline"
tags : [requirements,SWEN90009]
---
{% include JB/setup %}

## Technical Natural Language

#### Stylistic rules for natural language specification

* Motivate first, summarize after
* Define concepts before using them
* One requirement per sentence
* Keep sentences short
* Avoid unnecessary jargon and acronyms
* Use ‘shall’ for mandatory and ‘should’ for desirable statements
* Use examples to clarify abstract statements
* Use bulleted lists for explaining related items that detail conditions
* Use diagrams to simplify complex textual descriptions
* Use figures to provide visual overviews and emphasize key points
* Use tables to collect related facts
* Avoid complex combinations of conditions with nested or ambiguously associated conditions

#### Errors in Requirements

1. Omission    
    * Problem space aspect feature not stated by any requirement.       
      &nbsp; &bull; Missing objective, requirememnt or assumption.     
    * Very hard to detect.
2. Contradiction    
    * Requirements defining a problem space feature in an incompatible way.    
    * Related to conflicting viewpoints.    
    &nbsp;Train doors must always be kept closed between stations.    
    &nbsp;Train doors must be opened once a train is stopped after an emergency signal.
3. Inadequacy    
    * Requirement not adequately stating a problem world feature.
4. Ambiguity
    * Train doors shall be opened as soon as the train is stopped at a platform.
5. Unmeasurability


#### Flaws in requirements
1. Noise. Requirements conveys no information on any problem world feature.
2. Overspecification. Requirements stating a feature not pertaining to the problem space but to the solution space.
3. Unfeasibility. Requirements cannot be implemented within the assigned budget, schedule or development platform.
4. Unintelligibility. E.g. A requirement statement containing five acronyms.
5. Poor structuring
6. Forward reference. Requirement making use of problem space features that are not defined yet.
7. Remorse(悔恨). Requirement stating a problem world feature too late or incidentally.
8. Poor modifiability. Requirements whose modification may need to be globally propagated throughout the specification.
9. Opacity(不透明). Requiremewnt whose rationale, authoring or dependencies are invisible.


#### Quality factors in Requirements

1. Completeness    
    * Requirement documentation is sufficient to ensure that the system-to-be will satisfy all its objectives (including quality goals).     
    * Dedicated requirement to prevent undesirable effects.    
    * Describe the output for all possible inputs.    
    * Sufficient detail to allow for development.   
2. Consistency
    * Compatibility of all requirements, assumptions and domain properties.
3. Adequacy
    * Requirements address the actual needs system-to-be.
    * Correctly describe laws in the problem space. Environmental assumptions must be realistic.
4. Unambiguity
5. Measureability
6. Pertinencwe (针对性，相关性). Requirements model elemets of the problem space, not the solution space.
7. Feasibility. Requirements must be realizable.
8. Comprehensibility
9. Good structuring.
10. Modifiability.
11. Traceability. Context of requirements should be easy to retrieve.



