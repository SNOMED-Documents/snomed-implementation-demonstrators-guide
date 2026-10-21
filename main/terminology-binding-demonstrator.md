# Terminology Binding Demonstrator

The **Terminology Binding Demonstrator** is a sandbox for building clinical data-entry forms and binding each question to SNOMED CT - interactively, with no coding required. It's built for implementers, clinical informaticists, and anyone learning how terminology binding works.

**Try it here:** [https://ihtsdo.github.io/sct-implementation-demonstrator/#/sandbox](https://ihtsdo.github.io/sct-implementation-demonstrator/#/sandbox)

{% hint style="info" %}
This guide walks through every part of the sandbox, from connecting a terminology server to previewing your form as FHIR output. No prior SNOMED CT or FHIR experience is assumed.
{% endhint %}

## What you'll learn

* How to connect to a FHIR terminology server and choose a SNOMED CT edition
* How to build a question and bind it to SNOMED CT as its meaning
* How to choose the way an answer is captured, and where its codes come from
* How to save your work and preview it as JSON, a FHIR Bundle, and a FHIR Questionnaire

## Anatomy of a binding

Every question on a form is one **binding**, made of three parts working together:

<table><thead><tr><th width="205.15411376953125">Part</th><th>What it is</th></tr></thead><tbody><tr><td><strong>Question</strong></td><td>The display text the respondent sees, plus an optional <strong>question code</strong> - a SNOMED CT concept that captures the meaning of the question, so downstream systems know exactly what was asked.</td></tr><tr><td><strong>Answer type</strong></td><td>The input control: text box, decimal, checkboxes, autocomplete, and more - see <a href="terminology-binding-demonstrator.md#step-3-choose-an-answer-type">Step 3</a>.</td></tr><tr><td><strong>Binding source</strong></td><td>For coded answers, where the valid options come from - an ECL expression or a predefined value set - see <a href="terminology-binding-demonstrator.md#step-4-bind-coded-answers-to-snomed-ct">Step 4</a>.</td></tr></tbody></table>

## The toolbar, at a glance

<table><thead><tr><th width="204.37640380859375">Button</th><th>What it does</th></tr></thead><tbody><tr><td><strong>New binding</strong></td><td>Add a new question to the form</td></tr><tr><td><strong>Upload form</strong></td><td>Reopen a form you saved earlier</td></tr><tr><td><strong>Example</strong></td><td>Load the tool's built-in worked example - a ready-made appendicitis intake form - so you can inspect a complete binding set</td></tr><tr><td><strong>Clear</strong></td><td>Wipe the current form and start over</td></tr><tr><td><strong>View generated data</strong> / <strong>Download form</strong></td><td>Appear once your form has at least one binding - see <a href="terminology-binding-demonstrator.md#step-5-save-and-reload-your-work">Step 5</a> and <a href="terminology-binding-demonstrator.md#step-6-see-your-generated-output">Step 6</a></td></tr></tbody></table>

{% stepper %}
{% step %}
### Connect your terminology server and edition

Open the menu (the three lines in the top-left corner) to configure where the tool gets its SNOMED CT data from, before you start building.

| <p><br><sub>Settings panel</sub></p> | <p><br><sub>Server list</sub></p> | <p><br><sub>Edition &#x26; version</sub></p> |
| :----------------------------------: | :-------------------------------: | :------------------------------------------: |

* **FHIR Term Server:** pick which terminology server the tool queries.
* **Edition:** pick a SNOMED CT edition (for example, the International Edition or a national extension) and a release date.
* **Language:** pick the display language for concept search results.
{% endstep %}

{% step %}
### Create a question

Click **New binding**. A Properties panel opens on the right, next to your form:

* **Question text:** the display label the respondent sees.
* **Question code:** search and select a SNOMED CT concept; this is the meaning bound to the question.
* **Restrict to Observables:** narrows the concept search to observable entities, useful for lab-style questions.
* **Allow Repeating:** lets the respondent add multiple answers to this question.
* **Note:** an internal comment, not shown to the respondent.
{% endstep %}

{% step %}
### Choose an answer type

Every answer type falls into one of two groups.

#### **Coded - bound to SNOMED CT**

| Answer type                   | Notes                               |
| ----------------------------- | ----------------------------------- |
| Autocomplete                  | Recommended for large value sets    |
| Checkboxes                    | A single coded checkbox             |
| Checkbox - multiple selection | Pick several coded options          |
| Multi-prefix search select    | Search across multiple code systems |
| Options                       | A short, fixed coded list           |
| Select (Single)               | Coded dropdown, one answer          |
| Select (Multiple)             | Coded dropdown, several answers     |

#### **Structural / free-form**

| Answer type    | Notes                                             |
| -------------- | ------------------------------------------------- |
| Text box       | Free text, not coded                              |
| Decimal        | Numeric value with decimals                       |
| Integer        | Whole numeric value                               |
| Section header | A label to group questions - not an answer at all |
{% endstep %}

{% step %}
### Bind coded answers to SNOMED CT

For any coded answer type, you choose where its valid options come from:

<table><thead><tr><th width="130.98577880859375"></th><th>ECL expression</th><th>Predefined value set</th></tr></thead><tbody><tr><td><strong>How it works</strong></td><td>Define the value set on the fly with an expression (e.g. descendants of a concept)</td><td>Point to a value set that already exists on the connected terminology server</td></tr><tr><td><strong>Strength</strong></td><td>Flexible - adjust the query any time without touching the server</td><td>Reuses a standardized, governed list, consistent across forms</td></tr><tr><td><strong>Best for</strong></td><td>Narrow, one-off, or highly specific answer sets</td><td>A question where a shared value set already exists</td></tr></tbody></table>

{% hint style="info" %}
Not sure which to use? Reach for a predefined value set if one already exists for this question; use ECL when you need something more specific.
{% endhint %}
{% endstep %}

{% step %}
### Save and reload your work

{% hint style="warning" %}
**Nothing is saved automatically.** If you close or refresh the tab without downloading, your form is gone.
{% endhint %}

* **Download form:** save your current form as a `.json` file to your computer.
* **Upload form:** reopen a form you downloaded earlier, to keep editing or to share it.
* **Example:** loads the tool's ready-made appendicitis form, a good reference for what a finished, saved form looks like.
{% endstep %}

{% step %}
### See your generated output

Click **View generated data** at any time to see three live representations of your form:

<table><thead><tr><th width="272.9027099609375">Tab</th><th>What it shows</th></tr></thead><tbody><tr><td><strong>Data collected from form</strong></td><td>A plain JSON snapshot of every question and its current answer</td></tr><tr><td><strong>Data collected (FHIR Bundle)</strong></td><td>The same answers packaged as a standards-based FHIR transaction Bundle</td></tr><tr><td><strong>FHIR Questionnaire</strong></td><td>Your form's structure itself, expressed as a FHIR Questionnaire resource</td></tr></tbody></table>
{% endstep %}
{% endstepper %}

## Putting it together - a worked example

A short symptom-check form shows every binding option working together:

<table><thead><tr><th width="56.9246826171875">#</th><th>Question</th><th>Meaning (question code)</th><th>Answer type</th><th>Binding source</th></tr></thead><tbody><tr><td>1</td><td>Reason for visit</td><td> (free text)</td><td>Text box</td><td>n/a</td></tr><tr><td>2</td><td>Symptoms</td><td>e.g. a finding/symptom concept</td><td>Checkbox - multiple selection</td><td>ECL or value set</td></tr><tr><td>3</td><td>Temperature</td><td>a vital-sign concept</td><td>Decimal</td><td>n/a</td></tr><tr><td>4</td><td>Smoking status</td><td>a tobacco-use concept</td><td>Select (Single)</td><td>Predefined value set</td></tr><tr><td>5</td><td>Follow-up needed</td><td> (structural)</td><td>Select (Single)</td><td>Options (Yes / No)</td></tr></tbody></table>

This example is illustrative - build it yourself to practice, or click **Example** in the toolbar to explore a fully worked, real form.

## Quick reference

**Toolbar:** New binding (add a question) · Upload form (reopen) · Download form (save) · View generated data (preview) · Example (built-in sample) · Clear (start over)

**Binding source:** ECL expression (flexible, computed on the fly) · Predefined value set (reused from the terminology server)

**Answer types - coded:** Autocomplete, Checkboxes, Checkbox (multiple), Multi-prefix search select, Options, Select (Single / Multiple)

**Answer types - structural:** Text box, Decimal, Integer, Section header

## Tips

* Start with **New binding**, or click **Example** to explore a finished form first.
* Download your form often - nothing is saved automatically.
* Use **Restrict to Observables** to narrow concept search when your question is a lab-style observation.
* Use **View generated data** to check your output matches what you expect before sharing a form.
* Switch terminology server or edition any time to test against a different national extension.

_SNOMED CT Implementation Demos - Terminology Bindings Sandbox_\
[https://ihtsdo.github.io/sct-implementation-demonstrator/#/sandbox](https://ihtsdo.github.io/sct-implementation-demonstrator/#/sandbox)
