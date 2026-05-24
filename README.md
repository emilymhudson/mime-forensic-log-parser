# Advanced MIME Telemetry & Feature Extraction Engine

## Overview
This repository houses a deterministic, Object-Oriented parsing engine designed to deconstruct RFC 5322 formatted email envelopes. Built to resolve detection layer "payload blindness," this engine serves as the Layer 1 ingestion architecture for multi-modal deep learning threat detection systems. It systematically normalizes unstructured text, maps network topology, and isolates binary artifacts to generate a structured JSON telemetry schema optimized for Late Fusion machine learning pipelines.

## Core Architectural Capabilities

* **Linguistic Obfuscation Detection:** Employs heuristic evaluation to detect advanced adversarial text manipulation designed to bypass Secure Email Gateways (SEGs), including zero-width character injection (`\u200B-\u200D`) and high-density URL embedding.
* **Authentication Topology Mapping:** Automatically extracts and evaluates standard routing protocols (SPF, DKIM, DMARC) and isolates IPv4 routing nodes for downstream graph analytics.
* **Multi-Modal Payload Isolation:** Walks complex multipart MIME boundaries to isolate and hash (SHA-256) binary payloads (images, audio, executables), preparing them for independent evaluation via Convolutional Neural Networks (CNNs) and Transformer architectures.
* **Data Normalization:** Strips HTML formatting, sanitizes textual inputs, and extracts embedded domains to prep data strictly for Natural Language Processing (NLP) tokenization.

## The JSON Telemetry Schema
The engine outputs a highly structured, multi-dimensional JSON object designed for direct ingestion into analytical data lakes (Splunk, Google BigQuery) or feature arrays for machine learning models. 

**Schema Output Includes:**
* `network_topology`: Extracted SPF/DKIM/DMARC statuses.
* `linguistic_features`: Tokenization length, domain extraction, and sanitized NLP-ready text.
* `binary_artifacts`: Filesize, content-type mapping, and cryptographic hashes of isolated attachments.
* `obfuscation_flags`: Array of triggered heuristic evasion warnings.

## Execution & Usage
The engine is completely self-contained and requires standard Python libraries to ensure secure, offline processing of potentially malicious artifacts.

```bash
# Execute the engine against a raw .eml file or standard string input
python advanced_parser.py
