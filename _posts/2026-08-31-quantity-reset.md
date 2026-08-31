---
layout: post
title: "Quantity Reset"
---

## Preserving user intent in complex ERP workflows

### Executive summary

In an ERP system, changing a product in a document unexpectedly reset the manually calculated quantity. For users working with complex orders, this meant losing work and having to repeat calculations.

The problem looked small, but the underlying product question was broader:

> **How should the system behave when a user changes one part of a document without intending to change the work they have already done?**

I investigated the problem through observation of a real client's work, analysis of existing user requests, forum discussions, competitor analysis, a first-click test with 184 participants, and moderated usability testing of three prototypes.

The research showed that there was no single obvious place where users expected to control this behaviour. Instead of forcing one interaction model, I designed a persistent personal setting and made it discoverable through several relevant entry points.

The solution was released in version 3.0.2 with three behaviour options: reset quantity to zero, reset it to one, or do not reset it.

A subsequent iteration addressed a related inconsistency: when **“Do not reset”** was selected, newly created rows received a quantity of zero. This was changed to one in version 3.0.5.

After the second iteration, no further user requests or feedback about this mechanism were received. No quantitative post-release impact was measured, so this is treated as a qualitative signal rather than a measured business outcome. With today's product analytics approach, I would instrument the workflow around product and quantity changes.

---

## 1. Business context

The product was **1C:Management of Our Firm (УНФ)**, an ERP system for small and medium-sized businesses.

ERP workflows often combine multiple pieces of information in a single document. Users may calculate quantities, prices, discounts or other values based on information that is already entered.

This creates an important UX requirement:

> **Changing one input should not unexpectedly destroy other work the user has already completed.**

The quantity-reset problem emerged in exactly this type of workflow.

---

## 2. The gap

When a user changed the product in a document's tabular section, the system reset the **Quantity** field.

For a simple line item, this might appear harmless. But in many real workflows, the quantity is calculated manually before the product is selected or changed.

For example:

> A customer needs underlay for five rooms.
> 
> The seller calculates the required quantity for each room.
> 
> The customer then changes the requested thickness from 3 mm to 2 mm.
> 
> The seller changes the product — and the previously calculated quantity is lost.

The user did not intend to change the quantity.

The system nevertheless interpreted the product change as a reason to reset it.

This created a gap between **user intent** and **system behaviour**.

Users developed workarounds, such as copying a row before changing the product so that the calculated quantity would not be lost. This added an unnecessary step to an already complex workflow.

### The product problem

**The system protected its internal logic at the expense of preserving the user's work.**

The challenge was therefore not simply to “add a setting”, but to determine:

- whether users actually needed control over this behaviour;
    
- what behaviour they expected;
    
- where they would look for such a setting;
    
- and how the setting could be made discoverable without adding unnecessary complexity.
    

---

## 3. Research question

The initial research focused on two uncertainties.

### 01 — What do users actually need?

Was the request for “do not reset quantity” a specific preference, or did users need more control over the behaviour?

### 02 — Where would users look for the setting?

There were several plausible locations:

- general form settings;
    
- the Quantity field itself;
    
- the product field;
    
- a contextual command;
    
- a dedicated settings form.
    

The goal was not to assume the correct location, but to test where users naturally expected to find the control.

---

## 4. Research approach

I used several sources and methods to reduce different types of uncertainty.

|Question|Method|
|---|---|
|What problems do users encounter when working with key documents in our ERP system?|Observation of a real client's work (shadowing)|
|Is this a recurring user problem?|Analysis of previously submitted user requests|
|What do users and partners say about it?|Forum discussions and polls|
|How do other products solve similar problems?|Competitor analysis|
|Where would users look for the setting?|First-click test|
|Can users actually configure the behaviour?|Moderated usability testing|
|Which interaction model works best?|Rapid Iterative Testing and Evaluation (RITE)|

The competitor analysis included both direct and indirect products, including other 1C configurations and small-business products such as accounting, retail, CRM and business-management systems.

This combination allowed me to move from **problem validation** to **expectation discovery**, and further to **interaction validation**.

---

## 5. Discovery

### Observing the workflow

The initial understanding of the problem was strengthened by observing a real client's work.

This helped reveal the practical context behind the seemingly simple quantity reset: users can perform calculations before they have finalised the product selection, and changing the product does not necessarily mean that they want to recalculate the quantity.

This observation helped frame the problem around **preserving user intent**, rather than simply changing a field's default behaviour.

### Existing user feedback

The starting point was not a new feature idea created by the design team.

The project was initiated by existing user needs and requests.

Users had already developed workarounds to avoid losing quantity values when changing a product. This indicated that the current behaviour was creating real friction rather than being merely a theoretical UX issue.

### Competitive analysis

I also analysed how comparable products handled similar situations.

The analysis covered:

- 1C:Accounting;
    
- 1C:Trade Management;
    
- 1C:Retail;
    
- Kontur.Elba;
    
- My Business;
    
- My Warehouse;
    
- Bitrix24.
    

The full competitive analysis was part of the internal working documentation and therefore cannot be published.

The purpose was to understand the existing interaction patterns and expectations around configurable behaviour.

---

## 6. Where would users look?

I ran a first-click test with **184 participants**.

![The fist-click test result](/portfolio/assets/quantity-reset/image2.png)

The participants were asked to identify where they would look for the control.

The results were distributed across several locations:

|First choice|Participants|
|---|--:|
|Settings button in the form header|**26%**|
|Quantity column|**17%**|
|Product column|**11%**|
|Other locations|**46%**|

### What this told me

There was no dominant mental model.

Users could reasonably interpret the problem as:

- a **form setting**;
    
- a **Quantity setting**;
    
- or a **product-related behaviour**.
    

This was important because a single-entry solution based only on the designer's assumption could easily become a discoverability problem.

Instead of asking:

> “Which location is the correct one?”

I reframed the question as:

> **“How can we make the setting discoverable from the contexts in which users are likely to look for it?”**

---

## 7. From evidence to prototypes

Based on the research, I created three alternative prototypes for the Order document.

The setting could be reached through:

1. a **Settings** button in the document header;
    
2. the **More** menu above the Stocks tabular section;
    
3. the context menu of the **Quantity** column;
    
4. a dedicated form shown when changing a product if the current quantity differed from the configured value.
    

The goal was not to decide theoretically which location was best.

The prototypes allowed me to test whether users could actually find and use the mechanism.

---

## 8. Usability validation

I conducted remote, moderated usability testing with four participants:

- consultant;
    
- accountant;
    
- director;
    
- merchandiser.
    

The hypothesis was:

> **Users will be able to find and configure the quantity-reset behaviour.**

The result was positive:

**All four participants were able to configure the behaviour.**

This provided evidence that the proposed interaction model was understandable enough for users with different roles and backgrounds.

---

## 9. The product decision

The research led to a shift from a single hard-coded behaviour to a **user-configurable behaviour**.

The final model introduced a personal setting:

**“Reset quantity when changing the product”**

with three options:

- **Reset to zero**
    
- **Reset to one**
    
- **Do not reset**
    

This was an important product decision.

Rather than deciding that one behaviour was universally correct, the product acknowledged that different users and workflows have different expectations.

### Why a personal setting?

The behaviour concerns the user's working style rather than a document-specific business rule.

A persistent personal setting allows the system to adapt to the user's preference without requiring them to configure the behaviour repeatedly.

---

## 10. Making the setting discoverable

Because the research showed several competing expectations about where the setting should live, the final solution provided multiple discovery paths.

When a product is changed, users can be presented with a dialog asking what to do with the quantity:

- reset to one;
    
- reset to zero;
    
- or do not reset.
    

The user can also choose:

> **“Do not show again (remember the selected value)”**

This supports both first-time discovery and subsequent uninterrupted work.

![The dialog asking what to do with the quantity](/portfolio/assets/quantity-reset/image1en.png)

To change the setting later, users can access it through several paths:

- **Personal settings** — a familiar place for configuring personal preferences across an ERP system;
    
- the **Settings** command in document forms — a contextual location where other form settings are available;
    
- the context menu when the **Quantity** column is active — the closest location to the data being changed, although this cannot be the only entry point because context menus are not used by everyone.
    

The result is a single underlying setting with multiple contextual discovery paths.

---

## 11. The second iteration

The first release solved the original problem, but the new configuration exposed another inconsistency.

When the user selected:

> **Do not reset**

a newly created row received a quantity of **0**.

This was technically consistent with the previous behaviour, but it was inconsistent with the user's likely expectation for a new line containing a single product or service.

A new user request emerged around this behaviour.

The next iteration therefore changed the default value for new rows from:

**0 → 1**

when **“Do not reset”** was selected.

At the same time, the interaction model was simplified:

- if the user had already configured the quantity-reset behaviour, the choice dialog was no longer shown;
    
- the dialog remained relevant only when the setting had not yet been configured.
    

---

## 12. Outcome

The project resulted in two iterations.

### Version 3.0.2

Users gained control over what happened to quantity when changing a product:

**Zero / One / Do not reset**

The setting was made discoverable through multiple contextual entry points.

### Version 3.0.5

The behaviour was refined further:

- new rows receive **1** instead of **0** when “Do not reset” is selected;
    
- unnecessary choice dialogs are removed once the user has configured the behaviour.
    

### Post-release signal

After the second iteration, **no further user requests or feedback related to this mechanism were received**.

There was no quantitative post-release measurement of task time, error rate or adoption, so I would not claim a measured productivity improvement.

However, the absence of further requests or complaints provides a **qualitative signal that the identified friction had been addressed sufficiently for users to stop raising the issue**.

---

## 13. Product thinking demonstrated

This case demonstrates several aspects of my product approach.

### Understand before changing

The feature was grounded in observation of a real workflow, existing user requests, forum discussions and competitive analysis rather than starting from a predefined UI solution.

### Use evidence to reduce uncertainty

Different methods answered different questions:

**Observation →** what does the problem look like in a real workflow?

**User requests →** is there a recurring problem?

**Competitive analysis →** what patterns already exist?

**First-click test →** where do users expect the control?

**Usability testing →** can users actually configure it?

### Preserve useful complexity

The ERP product serves different roles and workflows. Instead of eliminating the variation by imposing one behaviour, the solution allowed users to choose the behaviour that fits their work.

### Show learning loops

The project did not end with the first implementation.

**Research → prototype → validation → release → new friction → iteration**

This is the part of the project I consider most important from a product perspective.

---

## 14. Evidence at a glance

|Evidence|Result|Role in decision|
|---|---|---|
|Observed behaviour of a real user|Problem identified in a real workflow|Trigger for subsequent research|
|Existing user requests|Repeated friction around quantity reset|Validated the problem|
|Forum discussions|User and partner perspectives|Expanded understanding of the need|
|Competitor analysis|Multiple interaction patterns|Informed solution exploration|
|First-click test|184 participants|Revealed distributed expectations|
|Usability testing|4 participants, all successful|Validated the proposed interaction|
|Release 3.0.2|Configurable quantity behaviour|Solved the original problem|
|Release 3.0.5|New-row quantity changed 0 → 1|Addressed an adjacent workflow issue|
|Post-release feedback|No further requests or feedback|Qualitative signal of resolution|

---

## 15. Methods

**Research**

- Shadowing
    
- User-request analysis
    
- Forum research
    
- Competitor analysis
    
- First-click testing
    
- Moderated usability testing
    

**Design**

- Rapid prototyping
    
- Multiple entry-point exploration
    
- Iterative refinement
    

**Product**

- Personalisation
    
- Configuration design
    
- Discoverability
    
- Behavioural consistency
    
- Post-release iteration
    

---

## 16. Product Value Loop

This project is an example of the way I approach product problems:

**Problem**

↓

**Understand the user and system context**

↓

**Identify uncertainty**

↓

**Collect evidence**

↓

**Make a product decision**

↓

**Prototype**

↓

**Validate**

↓

**Release**

↓

**Observe what happens next**

↓

**Iterate**

The important part is not the particular research method.

The important part is keeping the loop connected to the product decision.

---

# Reflection

This project changed how I think about UX work in complex enterprise software.

The most valuable outcome was not the setting itself, but the process of turning a seemingly small interaction problem into a product decision. The original issue was simple: changing a product could unexpectedly destroy a quantity the user had already calculated. Research showed that the problem was not only about the reset behaviour itself, but also about user expectations, discoverability and the different ways people work with the same ERP workflow.

The project also reinforced the importance of **iterative validation**. The first release solved the original problem, but it exposed another inconsistency in the surrounding workflow: when “Do not reset” was selected, new rows still received a quantity of zero. The second iteration addressed this and simplified the interaction by removing unnecessary prompts once the user's preference had been configured.

One limitation of the project was that we did not have product instrumentation to quantify the impact after release. The absence of further user requests or feedback after the second iteration provided a useful qualitative signal, but it could not tell us how much time or effort the change actually saved.

With today's product analytics approach, I would instrument the workflow around product and quantity changes. In particular, I would measure:

- **Quantity re-entry rate** — how often users have to enter the quantity again after changing a product;
    
- **Time to re-enter quantity** — the time spent recovering from an unwanted reset;
    
- **Quantity correction rate** — how often users change the quantity after the system has automatically set it;
    
- **Setting adoption and preference distribution** — how many users configure the behaviour and which option they choose;
    
- **Document completion time** — whether reducing this friction has a measurable effect on the overall document-entry workflow.
    

These measurements would allow the team to connect the UX problem to actual product behaviour and quantify the impact of the solution.

This changed an important part of how I think about product work:

> **Qualitative research helps us understand why a problem matters and what users need. Product analytics helps us understand how often it happens, how much it costs, and whether the solution actually improved the workflow.**

The goal is therefore not to stop at **“Are users still complaining?”**, but to move towards **“Did the behaviour improve, for whom, and by how much?”**

For complex products, I see this as a continuous loop:

**Understand → validate → decide → release → measure → learn → iterate.**

The aim is not to remove complexity from enterprise software. It is to make that complexity **predictable, understandable and controllable for the people who use it**.
