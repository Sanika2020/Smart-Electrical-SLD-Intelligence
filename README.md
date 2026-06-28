# Smart Electrical SLD Intelligence

### AI Based Interpretation of Single Line Diagrams Using Computer Vision and Graph Analysis

## Overview

Electrical utilities, substations, and power distribution networks are commonly represented using Single Line Diagrams (SLDs). These diagrams contain critical information about transformers, feeders, power sources, and network connectivity. However, most SLDs exist as static images or PDFs that require manual interpretation by engineers.

This project presents an AI-powered framework that automatically analyzes SLD images and converts them into structured, machine-readable electrical network representations. The system combines deep learning, computer vision, and graph analysis techniques to identify electrical components, infer connections, determine source-feeder relationships, and generate JSON outputs for downstream applications.

## Problem Statement

Manual interpretation of Single Line Diagrams is:

* Time consuming
* Prone to human error
* Difficult to scale for large substations
* Not directly compatible with digital platforms such as SCADA, GIS, and Digital Twins

The objective of this project is to automatically convert SLD images into structured electrical network data.

## Key Features

* Transformer detection using YOLOv8
* Electrical line extraction using OpenCV
* Edge detection using Canny Operator
* Connection extraction using Hough Transform
* Graph-based network modeling
* Source identification
* Feeder identification
* Structured JSON output generation
* Annotated visualization output

## Dataset

The model was trained using multiple publicly available electrical schematic datasets and manually annotated and created dataset from research papers and electrical department papers from Roboflow Universe.

Datasets Used:

* SLD Detection Dataset
* Electrical Diagrams Detection Dataset
* Schematic Dataset
* Transformer Detection Dataset

All transformer related classes were merged into a unified transformer class to simplify detection and improve consistency across datasets.


## Methodology

### 1. Object Detection

YOLOv8 is used to detect transformers in SLD images.

The model outputs:

* Bounding boxes
* Confidence scores
* Component locations

---

### 2. Edge Detection

Canny Edge Detection identifies significant image gradients and extracts edges corresponding to electrical wiring and diagram structures.

---

### 3. Line Detection

The Probabilistic Hough Transform converts edge information into line segments representing electrical connections.

---

### 4. Graph Construction

Detected transformers are represented as nodes.

Detected line segments are represented as edges.

Together they form a graph:

G = (N, E)

where:

* N = Electrical Components
* E = Connections

---

### 5. Connectivity Analysis

Breadth First Search (BFS) is used to traverse the graph and determine component relationships.

A distance based heuristic fallback mechanism is introduced to improve robustness when line detection is incomplete.

---

### 6. Source and Feeder Identification

The top most detected node is identified as the source.

Nodes connected to the source are classified as feeders.

---

## Sample Output

### Annotated Image

The system generates:

* Transformer bounding boxes
* Connection lines
* Source indication
* Feeder visualization

### JSON Output

```json
{
  "source": 2,
  "feeders": [1, 3],
  "nodes": [
    {
      "id": 0,
      "type": "transformer"
    }
  ],
  "connections": [
    [0, 3],
    [1, 2]
  ]
}
```


## Real-World Applications

### Smart Substations

Automatic digitization of legacy substation drawings.

### SCADA Integration

Converts static diagrams into structured data suitable for monitoring systems.

### GIS Mapping

Maps electrical assets into geospatial systems.

### Digital Twin Creation

Provides machine-readable network topology for digital twin platforms.

### Asset Management

Automatically extracts network information from engineering drawings.

### Power System Planning

Assists engineers in understanding and analyzing large electrical networks.

## Project Structure

```text
Smart-Electrical-SLD-Intelligence/
│
├── dataset/
├── merged_dataset/
├── train/
├── test/
├── models/
├── outputs/
├── notebooks/
├── README.md
└── requirements.txt
```

## References

* Intelligent Digitization of Substation One-Line Diagrams Based on Computer Vision
* Analysis of Single Line Diagrams Using AI
* Electrical Diagram Detection Datasets (Roboflow)
* YOLOv8 Documentation
* OpenCV Documentation

---

## Author

Sanika V H
---

## License

This project is intended for educational and research purposes.
