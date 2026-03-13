# MSc MLS Thesis Coordination Dashboard

**MSc Medical Laboratory Science Program**  
**College of Health Sciences — Gulf Medical University**

A web-based coordination dashboard designed to support the management of MSc Medical Laboratory Science thesis activities. The system provides a centralized interface for tracking student progress, monitoring milestones, coordinating supervisors, and automating essential communication tasks.

This dashboard supports the operational workflow of the **Thesis I and Thesis II courses**, enabling structured oversight of proposal development, milestone completion, and thesis supervision.

---

# Project Purpose

Thesis coordination requires managing multiple students, supervisors, deadlines, and administrative processes simultaneously. This dashboard was developed to provide a structured coordination system that helps program leaders:

- monitor student research progress
- track thesis milestones
- manage supervisor assignments
- automate communication with students and supervisors
- generate program-level progress summaries

The goal is to **reduce administrative workload while improving visibility and coordination across the thesis process**.

---

# Key Features

## Student Tracking

Centralized registry of MSc MLS students including:

- student name
- registration number
- student email
- assigned supervisor
- co-supervisor (if applicable)
- current thesis stage
- milestone completion status

---

## Milestone Monitoring

The dashboard tracks key stages of the thesis lifecycle:

1. Proposal development
2. Proposal presentation
3. IRB / ethics approval
4. Data collection
5. Progress report submission
6. Thesis writing
7. Final defense

Milestones can be reviewed at both the **individual student level and cohort level**, helping coordinators identify delays early.

---

## Supervisor Coordination

The system allows monitoring of supervisor engagement and workload including:

- number of students per supervisor
- pending feedback
- overdue milestone reviews
- supervision distribution

This helps maintain **equitable supervision allocation and timely feedback cycles**.

---

## Automated Communication

The dashboard integrates automated email functionality allowing the coordinator to:

- request ORCID information
- request milestone reflections
- send follow-up reminders
- request supervisor progress updates

All communications are sent using the official program signature.

---

## Reflection and Reporting

Students submit structured reflections at key stages including:

- proposal presentation
- progress reporting
- thesis completion stages

Supervisor feedback and student reflections can be summarized to generate program-level reports.

---

# System Architecture

The MSc MLS Thesis Coordination Dashboard is designed as a **lightweight web system deployable through GitHub Pages**, requiring no dedicated server infrastructure.

### Core Modules

**Dashboard Interface**  
Provides a real-time overview of:

- active students
- milestone completion
- supervisor distribution
- pending coordinator actions

**Student Registry Module**  
Stores core information for each student including identity, supervisor assignment, and thesis stage.

**Milestone Tracking Engine**  
Monitors completion of thesis stages and highlights overdue tasks.

**Communication Automation Layer**  
Uses predefined email templates to trigger program communications.

**Reporting Module**  
Generates cohort-level summaries including supervision load and milestone progress.

---

# Data Structure

The dashboard is built around a structured dataset representing each MSc MLS student.

Example data fields:

```
Student Name
Registration Number
Student Email
Supervisor Name
Supervisor Email
Co-Supervisor Name
ORCID Status
Thesis Stage
Proposal Status
IRB Status
Progress Report Status
Defense Status
Reflection Submissions
Supervisor Feedback
```

---

# Email Communication Signature

Automated emails use the following standardized program identity:

**Dr. Salma Elnour Rahma**  
Associate Professor of Microbiology, Thesis Coordinator  
BSc, MSc, PhD (Microbiology), MPhil (Health Professions Education)

MSc Medical Laboratory Science Program  
College of Health Sciences  
Gulf Medical University

---

# Deployment Guide

The dashboard is designed to be hosted using **GitHub Pages**.

### Step 1 — Repository Setup

Create a repository:

```
msc-mls-thesis-dashboard
```

Add project files:

```
index.html
README.md
assets/
styles/
scripts/
```

---

### Step 2 — Enable GitHub Pages

Navigate to:

```
Repository Settings → Pages
```

Set source:

```
Deploy from branch → main
```

GitHub will generate a public dashboard URL.

---

### Step 3 — Upload Dashboard

Upload the main dashboard interface as:

```
index.html
```

Once deployed, the coordination dashboard becomes publicly accessible.

---

# Optional Integrations

The system can be extended with:

**EmailJS** – send automated emails directly from the dashboard.

**Google Forms** – collect reflections and supervisor reports.

**Google Apps Script** – synchronize responses from spreadsheets.

---

# Use Case

This system was designed to support **postgraduate thesis coordination in health sciences programs**, particularly where multiple students and supervisors require structured monitoring.

Although developed for the **MSc Medical Laboratory Science Program**, the structure can be adapted to other postgraduate research programs.

---

# License

This project is intended for **academic and educational coordination purposes**. Institutions are free to adapt and modify the system to suit their program needs.
