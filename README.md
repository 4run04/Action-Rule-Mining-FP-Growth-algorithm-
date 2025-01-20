# Action Rules Mining with FP-Growth

## Overview
This project implements an efficient action rules mining algorithm using a modified FP-Growth approach. The algorithm is designed to discover actionable patterns in classification datasets, specifically identifying sequences of actions that can potentially transform instances from an undesired state (negative class) to a desired state (positive class).

## Features
- Efficient FP-tree based pattern mining
- Precomputed support and confidence metrics for atomic actions
- Customizable support and confidence thresholds
- Vectorized operations for performance optimization
- Comprehensive rule extraction with support and confidence metrics
- Built-in data preprocessing and discretization

## Installation

### Requirements
```
pandas
ucimlrepo
```

Install the required packages using:
```bash
pip install pandas ucimlrepo
```

## Usage

### 1. Data Preparation
```python
from ucimlrepo import fetch_ucirepo
df = prepare_data()  # Handles missing values and discretization
```

### 2. Generate Atomic Actions
```python
atomic_action_sets = generate_all_possible_transitions(df)
```

### 3. Calculate Support and Confidence
```python
atomic_metrics = calculate_atomic_metrics(atomic_action_sets, positive_df, negative_df)
```

### 4. Build FP-Tree and Extract Rules
```python
fp_tree = FPTree()
fp_tree.build_tree(pruned_action_table)
rules = extract_action_rules_with_precomputed(fp_tree, atomic_metrics)
```

## Key Components

### FPNode Class
Represents a node in the FP-tree structure with:
- Action (feature, old_value, new_value)
- Count
- Parent/child relationships
- Next node pointer for header table

### FPTree Class
Implements the FP-tree structure with methods for:
- Tree construction
- Pattern mining
- Header table management
- Tree traversal

### Action Rule Extraction
- Identifies patterns that could transform instances from negative to positive class
- Calculates support and confidence metrics
- Provides sorted rules based on support and confidence

## Parameters

- `min_support`: Minimum support threshold for atomic actions (default: 4000)
- `min_confidence`: Minimum confidence threshold for rules (default: 0.1)
- Discretization: Numeric features are discretized into 3 bins (low, medium, high)

## Example Output

A typical action rule output looks like:
```
Rule: IF A1: low → high AND A2: medium → high
Support: 5000
Confidence: 0.75
```

This indicates that changing A1 from low to high AND A2 from medium to high has:
- Support of 5000 (frequency in the dataset)
- 75% confidence of transforming from negative to positive class

## Performance Optimization

The implementation includes several optimizations:
1. Precomputed metrics for atomic actions
2. Vectorized operations using pandas
3. Early filtering of low-support/confidence rules
4. Efficient tree traversal

## Dataset

The project uses the Credit Approval dataset from UCI ML Repository, which includes:
- Binary classification (approved/not approved)
- Mixed numeric and categorical features
- Missing value handling
- Automatic discretization of numeric features

## Contributing

Feel free to submit issues and enhancement requests. Follow these steps:
1. Fork the repository
2. Create a feature branch
3. Submit a pull request with a clear description of changes

## License

This project is licensed under the MIT License - see the LICENSE file for details.

---

For more detailed information about specific components or to request features, please open an issue in the repository.
