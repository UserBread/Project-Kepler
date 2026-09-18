# Core Data Model

The following concepts form the initial conceptual model.

```text
Dataset
   |
   +--> DatasetVersion
            |
            v
        Experiment
        /   |    \
       /    |     \
Hypotheses Analyses Models
       \    |     /
        \   |    /
         Critiques
             |
             v
          Findings
             |
             v
           Report
```

## Dataset

Represents a logical dataset.

Potential fields:

- ID
- Name
- Source
- Format
- Description

## DatasetVersion

Represents a specific immutable version of a dataset.

Potential fields:

- Version ID
- Dataset ID
- Content hash
- Schema
- Created timestamp

## Experiment

Represents an investigation performed by Kepler.

Potential fields:

- Experiment ID
- Dataset version
- Question
- Configuration
- State
- Start/end timestamps

## Hypothesis

Represents a testable proposition generated during an investigation.

## Analysis

Represents a specific analytical operation.

## Model

Represents a trained or evaluated machine-learning model.

## Metric

Represents a quantitative evaluation result.

## Critique

Represents a methodological or interpretive issue identified by Kepler.

## Finding

Represents a conclusion supported by one or more pieces of evidence.

## Report

Represents the final human-readable output.
