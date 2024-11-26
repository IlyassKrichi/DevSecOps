# DevSecOps CI/CD Pipeline for Juice Shop

This repository contains a DevSecOps pipeline for automating the deployment and security scanning of the **OWASP Juice Shop** application. The pipeline uses GitHub Actions to perform Static Application Security Testing (SAST), Software Composition Analysis (SCA), Dynamic Application Security Testing (DAST), and Container Security scanning.

## Table of Contents

- [Overview](#overview)
- [Workflows](#workflows)
  - [DAST: OWASP ZAP](#dast-owasp-zap)
  - [SAST: Semgrep](#sast-semgrep)
  - [SCA: Snyk](#sca-snyk)
  - [Container Security: Grype](#container-security-grype)
  - [Reporting](#reporting)
- [Setup](#setup)
- [Usage](#usage)
- [Summary](#summary)

---

## Overview

This project sets up an automated pipeline that integrates security checks into the CI/CD process for the **OWASP Juice Shop**. Each component of the pipeline performs security checks on the application at various stages:

- **SAST**: Static code analysis using Semgrep to detect vulnerabilities in the codebase.
- **SCA**: Software Composition Analysis using Snyk to identify known vulnerabilities in third-party dependencies.
- **DAST**: Dynamic analysis using OWASP ZAP to test the application for runtime vulnerabilities.
- **Container Security**: Vulnerability scanning of the Docker container image using Grype.

All results from these security scans are aggregated into a single report for easy analysis.

---

## Workflows

### DAST: OWASP ZAP

The **Dynamic Application Security Testing** (DAST) workflow performs security scans on a running instance of the **OWASP Juice Shop** application using **OWASP ZAP**. This step checks for vulnerabilities during the execution of the application.

- **Steps**:
  1. Checkout the repository.
  2. Install dependencies.
  3. Start the app.
  4. Run ZAP scan on the app.
  5. Upload ZAP scan report.

See [dast.yml](.github/workflows/dast.yml).

### SAST: Semgrep

The **Static Application Security Testing** (SAST) workflow uses **Semgrep** to analyze the code for vulnerabilities without running the application. It checks for insecure coding practices or vulnerabilities in the source code.

- **Steps**:
  1. Checkout the repository.
  2. Install Semgrep.
  3. Run Semgrep scan and generate results.
  4. Upload SAST results.

See [sast.yml](.github/workflows/sast.yml).

### SCA: Snyk

The **Software Composition Analysis** (SCA) workflow scans third-party dependencies for vulnerabilities using **Snyk**. This helps identify known vulnerabilities in libraries used by the application.

- **Steps**:
  1. Checkout the repository.
  2. Set up Node.js.
  3. Install dependencies.
  4. Run Snyk to check for vulnerabilities.
  5. Upload SCA results.

See [sca.yml](.github/workflows/sca.yml).

### Container Security: Grype

The **Container Security** workflow uses **Grype** to scan the Docker image of the application for vulnerabilities, including those in the operating system and libraries.

- **Steps**:
  1. Checkout the repository.
  2. Build the Docker image.
  3. Run Grype scan on the image.
  4. Upload Grype scan results.

See [container.yml](.github/workflows/container.yml).

### Reporting

The **Reporting** workflow aggregates all security scan results (SAST, SCA, DAST, Container Security) into a single compressed report for easier analysis and tracking.

- **Steps**:
  1. Download the results from all workflows.
  2. Aggregate the results into a zip file.
  3. Upload the aggregated report.

See [report.yml](.github/workflows/report.yml).

---

## Setup

### Prerequisites

To use this pipeline, you'll need:

1. **GitHub Secrets**:
   - `SNYK_TOKEN`: Snyk API token for SCA.

2. **Node.js**: Version 20 (or a compatible version) should be installed for the application dependencies.

3. **Docker**: Docker must be installed to build and scan the Docker image.

4. **OWASP Juice Shop**: This pipeline is set up for scanning the Juice Shop application, which should be configured to run on port `3000`.

### How to Set Up

1. Clone the repository:
   
   ```bash
   git clone https://github.com/<your-username>/DevSecOps-JuiceShop.git
   cd DevSecOps-JuiceShop
   ```
3. Add your secrets to GitHub repository settings under Secrets.
4. Ensure the application runs locally before triggering scans:
   
   ```bash
   npm install
   npm start
   ```

### Usage

1. Triggering Workflows: The workflows are triggered automatically based on events like pushing to the main branch or opening pull requests. You can also manually trigger them through the GitHub Actions tab.
2. Viewing Results: After each workflow runs, the results will be uploaded as artifacts. You can download them from the Actions tab in GitHub.

### Summary

This DevSecOps CI/CD pipeline automates the security testing of the OWASP Juice Shop app, ensuring that code changes undergo rigorous checks at various stages of the development process. It includes SAST, SCA, DAST, and container security scanning with flexible, modular workflows.

Let me know if you need further customization or additional instructions!
