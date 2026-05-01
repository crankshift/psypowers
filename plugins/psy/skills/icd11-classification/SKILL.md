---
name: icd11-classification
description: Use when classifying mental health conditions, mapping symptoms to diagnostic codes, performing differential diagnosis, or referencing ICD-11 Chapter 06 (Mental, behavioural or neurodevelopmental disorders). Covers code structure 6A00-6E8Z, diagnostic criteria summaries, differential diagnosis decision trees, and ICD-11 vs DSM-5-TR differences.
---

# icd11-classification

ICD-11 Chapter 06 replaced ICD-10 Chapter V (F00-F99) with a restructured classification that better reflects current evidence. The coding moved from letter-based (F-codes) to block-based (6-prefix) and introduced dimensional approaches for personality disorders. This skill covers the full 6A00-6E8Z range with diagnostic pointers and differential logic.

## Fetch-first block

Before relying on the fallback data below, attempt to fetch current criteria:

```
WebFetch: https://icd.who.int/browse/2024-01/mms/en#334423054
```

If the fetch succeeds, use the live content — it may contain updates beyond the January 2024 revision annotated here. All criteria summaries below are based on ICD-11 MMS 2024-01.

## Code structure overview

ICD-11 Chapter 06 uses a hierarchical alphanumeric system. The first two characters are always `6` + letter. The third and fourth characters refine the category. Extensions after the dot provide further specificity.

| Block | Range | Category |
|---|---|---|
| 6A | 6A00–6A0Z | Neurodevelopmental disorders |
| 6A2 | 6A20–6A2Z | Schizophrenia or other primary psychotic disorders |
| 6A4 | 6A40–6A4Z | Catatonia |
| 6A6–6A8 | 6A60–6A8Z | Mood disorders |
| 6B0 | 6B00–6B0Z | Anxiety or fear-related disorders |
| 6B2 | 6B20–6B2Z | Obsessive-compulsive or related disorders |
| 6B4 | 6B40–6B4Z | Disorders specifically associated with stress |
| 6B6 | 6B60–6B6Z | Dissociative disorders |
| 6B8 | 6B80–6B8Z | Feeding or eating disorders |
| 6C2 | 6C20 | Disorders of bodily distress or bodily experience |
| 6C4 | 6C40–6C4Z | Disorders due to substance use |
| 6C7 | 6C70 | Impulse control disorders |
| 6C9 | 6C90 | Disruptive behaviour or dissocial disorders |
| 6D1 | 6D10–6D11 | Personality disorders and related traits |
| 6D3 | 6D30 | Paraphilic disorders |
| 6D5 | 6D50 | Factitious disorders |
| 6D7–6D8 | 6D70–6D8Z | Neurocognitive disorders |
| 6E | 6E00–6E8Z | Other/secondary mental or behavioural syndromes |

## Category details

### Neurodevelopmental disorders (6A00–6A0Z)

**Key codes:**
- 6A00 Disorders of intellectual development (mild/moderate/severe/profound)
- 6A01 Developmental speech or language disorders
- 6A02 Autism spectrum disorder
- 6A03 Developmental learning disorder
- 6A04 Developmental motor coordination disorder
- 6A05 Attention deficit hyperactivity disorder
- 6A06 Stereotyped movement disorder

**Essential features:** Onset during the developmental period. Significant difficulties in acquisition and execution of specific intellectual, motor, language, or social functions. Dimensional severity rather than categorical subtypes for ASD and intellectual development.

**Key differentiators:** Neurodevelopmental disorders are distinguished from acquired conditions by onset timing. ADHD requires symptom presence before age 12 (though diagnosis can occur later). ASD in ICD-11 drops Asperger's as a separate diagnosis — it is folded into ASD with specifiers for intellectual functioning and language ability.

**Common comorbidities:** ADHD + learning disorders, ASD + anxiety, ASD + ADHD (now explicitly allowed in ICD-11).

### Schizophrenia or other primary psychotic disorders (6A20–6A2Z)

**Key codes:**
- 6A20 Schizophrenia
- 6A21 Schizoaffective disorder
- 6A22 Schizotypal disorder
- 6A23 Acute and transient psychotic disorder
- 6A24 Delusional disorder
- 6A25 Symptomatic manifestations of primary psychotic disorders

**Essential features:** Core symptoms include positive (delusions, hallucinations, disorganised thinking/behaviour) and negative (blunted affect, avolition, alogia) symptoms. Schizophrenia requires >=1 month of symptoms including at least two core features, with one being delusions, hallucinations, or disorganised thinking.

**Key differentiators:** Schizoaffective disorder requires concurrent and equally prominent mood and psychotic episodes. Acute and transient psychotic disorder lasts <3 months. Delusional disorder features persistent delusions without other psychotic symptoms. Schizotypal disorder is reclassified here from personality disorders in ICD-10.

**Common comorbidities:** Substance use disorders, depression, anxiety, metabolic syndrome (often treatment-related).

### Catatonia (6A40–6A4Z)

**Essential features:** Psychomotor disturbance — stupor, catalepsy, waxy flexibility, mutism, negativism, posturing, stereotypies, agitation, grimacing, echolalia, echopraxia. Requires at least 3 features. ICD-11 classifies catatonia as its own block, not a subtype of schizophrenia.

**Key codes:**
- 6A40 Catatonia associated with another mental disorder
- 6A41 Catatonia induced by substances or medications
- 6A4Z Secondary catatonia syndrome

### Mood disorders (6A60–6A8Z)

**Bipolar disorders (6A60–6A6Z):**
- 6A60 Bipolar type I: at least one manic episode (elevated mood OR irritability + increased energy, lasting >=1 week or hospitalisation)
- 6A61 Bipolar type II: at least one hypomanic episode (>=4 days) + at least one depressive episode, no full mania
- 6A62 Cyclothymic disorder: chronic fluctuating mood disturbance (>=2 years) not meeting criteria for full episodes

**Depressive disorders (6A70–6A7Z):**
- 6A70 Single episode depressive disorder
- 6A71 Recurrent depressive disorder
- 6A72 Dysthymic disorder: depressed mood most days, >=2 years
- 6A73 Mixed depressive and anxiety disorder

**Essential features of depressive episode:** Depressed mood or loss of interest/pleasure, nearly every day, lasting >=2 weeks. Accompanied by changes in appetite/weight, sleep, psychomotor activity, fatigue, worthlessness/guilt, concentration difficulties, suicidal ideation/behaviour. Severity rated mild/moderate/severe based on symptom count, intensity, and functional impact.

**Key differentiators:** Mania vs hypomania — mania lasts >=1 week or causes hospitalisation and causes marked functional impairment; hypomania lasts >=4 days without severe impairment. Dysthymia vs recurrent depression — dysthymia is chronic but less severe. Mixed depressive and anxiety disorder is new in ICD-11 for subthreshold presentations.

**Common comorbidities:** Anxiety disorders (up to 60% with depression), substance use, personality disorder features.

### Anxiety or fear-related disorders (6B00–6B0Z)

**Key codes:**
- 6B00 Generalised anxiety disorder (GAD)
- 6B01 Panic disorder
- 6B02 Agoraphobia
- 6B03 Specific phobia
- 6B04 Social anxiety disorder
- 6B05 Separation anxiety disorder

**Essential features by disorder:**
- **GAD:** Marked apprehension or worry about everyday events, most days, >=several months. Accompanied by restlessness, muscle tension, autonomic symptoms, difficulty concentrating, irritability, sleep disturbance.
- **Panic disorder:** Recurrent unexpected panic attacks (sudden surge of fear with physical symptoms — palpitations, sweating, trembling, dyspnoea, chest pain) + persistent concern about recurrence or maladaptive behavioural change.
- **Agoraphobia:** Marked fear/anxiety about situations where escape is difficult (public transport, open spaces, enclosed spaces, crowds, being outside home alone). Avoidance or endurance with intense distress.
- **Specific phobia:** Excessive fear/anxiety about specific objects or situations (animals, heights, blood/injection, flying, etc.) disproportionate to actual danger. Immediate anxiety upon exposure.
- **Social anxiety disorder:** Marked fear of social situations where scrutiny is possible. Fear of negative evaluation. Avoidance or endurance with intense anxiety.
- **Separation anxiety disorder:** Excessive fear about separation from attachment figures, beyond developmentally appropriate, lasting >=several months in adults.

**Common comorbidities:** GAD + depression (very frequent), panic + agoraphobia, social anxiety + avoidant personality traits, multiple anxiety disorders co-occurring.

### Obsessive-compulsive or related disorders (6B20–6B2Z)

**Key codes:**
- 6B20 Obsessive-compulsive disorder
- 6B21 Body dysmorphic disorder
- 6B22 Olfactory reference disorder (new in ICD-11)
- 6B23 Hypochondriasis (health anxiety)
- 6B24 Hoarding disorder
- 6B25 Body-focused repetitive behaviour disorders (trichotillomania, excoriation)

**Essential features:** OCD: persistent, unwanted intrusive thoughts/images/urges (obsessions) and/or repetitive behaviours or mental acts performed to reduce distress (compulsions). Time-consuming (>=1 hour/day) or causes significant distress/impairment.

**Key differentiators:** OCD vs GAD — GAD worry is about real-life concerns; obsessions are experienced as intrusive and ego-dystonic. OCD vs psychosis — insight specifier in OCD ranges from good to absent, but even with absent insight the content is typically OCD-type themes (contamination, symmetry, harm) rather than bizarre delusions.

### Disorders specifically associated with stress (6B40–6B4Z)

**Key codes:**
- 6B40 Post-traumatic stress disorder (PTSD)
- 6B41 Complex post-traumatic stress disorder (Complex PTSD — new in ICD-11)
- 6B42 Prolonged grief disorder (new in ICD-11)
- 6B43 Adjustment disorder
- 6B44 Reactive attachment disorder
- 6B45 Disinhibited social engagement disorder

**Essential features:**
- **PTSD:** Exposure to extremely threatening/horrific event(s). Three core clusters: (1) re-experiencing in the present (flashbacks, nightmares with sense of event recurring now), (2) avoidance of reminders, (3) persistent sense of current threat (hypervigilance, exaggerated startle). Lasts >=several weeks.
- **Complex PTSD:** All PTSD criteria PLUS disturbances in self-organisation: (1) affect dysregulation, (2) negative self-concept (defeated, worthless, guilt/shame), (3) difficulties in relationships. Typically follows prolonged/repeated trauma.
- **Prolonged grief disorder:** Persistent pervasive grief response >=6 months after bereavement, exceeding social/cultural norms. Intense emotional pain, longing, preoccupation with the deceased.
- **Adjustment disorder:** Preoccupation with stressor and failure to adapt, arising within 1 month, usually resolving within 6 months after stressor ends.

**Key differentiators:** PTSD vs adjustment — PTSD requires a qualifying traumatic event + specific symptom clusters; adjustment is a broader, less specific reaction. Complex PTSD vs borderline PD — overlap in affect dysregulation and relationship difficulties, but Complex PTSD requires trauma exposure and has the core PTSD re-experiencing cluster.

### Dissociative disorders (6B60–6B6Z)

**Key codes:**
- 6B60 Dissociative neurological symptom disorder
- 6B61 Dissociative amnesia
- 6B62 Trance disorder
- 6B63 Possession trance disorder
- 6B64 Dissociative identity disorder
- 6B65 Partial dissociative identity disorder (new in ICD-11)
- 6B66 Depersonalisation-derealisation disorder

### Feeding or eating disorders (6B80–6B8Z)

**Key codes:**
- 6B80 Anorexia nervosa: significantly low body weight + restriction + fear of weight gain/body image disturbance
- 6B81 Bulimia nervosa: recurrent binge eating + compensatory behaviours + body shape/weight over-valuation
- 6B82 Binge eating disorder: recurrent binge eating without regular compensatory behaviours + marked distress
- 6B83 Avoidant-restrictive food intake disorder (ARFID — new in ICD-11 as separate code)
- 6B84 Pica
- 6B85 Rumination-regurgitation disorder

**Key differentiators:** AN vs BN — AN has significantly low body weight; BN typically normal/above normal weight. BED vs BN — BED has no regular compensatory behaviours. ARFID vs AN — ARFID has no body image disturbance.

### Disorders due to substance use (6C40–6C4Z)

Structured by substance: alcohol (6C40), cannabis (6C41), synthetic cannabinoids (6C42), opioids (6C43), sedatives/hypnotics/anxiolytics (6C44), cocaine (6C45), stimulants (6C46), synthetic cathinones (6C47), caffeine (6C48), hallucinogens (6C49), nicotine (6C4A), volatile inhalants (6C4B), MDMA (6C4C), dissociative drugs (6C4D), other (6C4E), multiple/unknown (6C4G-6C4H).

Each substance has sub-codes: .0 episode of harmful use, .1 harmful pattern of use, .2 dependence, .3 intoxication, .4 withdrawal, .5 substance-induced disorders (psychotic, mood, anxiety).

### Personality disorders and related traits (6D10–6D11)

**Major ICD-11 change:** Replaced categorical types (paranoid, schizoid, etc.) with a dimensional model.

- **6D10 Personality disorder:** Classified by severity — mild, moderate, severe. Requires: (1) pervasive disturbance in self-functioning (identity, self-worth, self-direction) and/or interpersonal functioning (empathy, intimacy, cooperation), (2) maladaptive patterns of cognition, emotional experience, emotional expression, behaviour, (3) present across situations, (4) present over extended period (>=2 years), (5) not better explained by another disorder or substance/medication.
- **6D11 Trait domain specifiers:** Negative affectivity, Detachment, Dissociality, Disinhibition, Anankastia. Apply one or more to the personality disorder diagnosis.
- **Borderline pattern qualifier:** Retained as a specifier given its clinical significance. Characterised by: unstable self-image, chronic emptiness, emotional reactivity, impulsivity, fear of abandonment, relationship instability, self-harm.

### Neurocognitive disorders (6D70–6D8Z)

- 6D70 Delirium
- 6D71 Mild neurocognitive disorder (does not significantly interfere with independence)
- 6D72 Amnestic disorder
- 6D80–6D8Z Dementia due to specific aetiologies (Alzheimer, vascular, Lewy body, frontotemporal, Parkinson, HIV, etc.)

### Other blocks

- **6C20 Disorders of bodily distress or bodily experience:** Replaces ICD-10 somatoform disorders. Focuses on distressing bodily symptoms + excessive attention/behaviour directed toward symptoms.
- **6C70 Impulse control disorders:** Pyromania, kleptomania, intermittent explosive disorder, compulsive sexual behaviour disorder (new in ICD-11).
- **6C90 Disruptive behaviour or dissocial disorders:** Oppositional defiant disorder, conduct-dissocial disorder.
- **6D30 Paraphilic disorders:** Only disorders causing distress or risk of harm — exhibitionistic, voyeuristic, frotteuristic, sadistic, masochistic, paedophilic, coercive. ICD-11 distinguishes paraphilias (not disorders) from paraphilic disorders.
- **6D50 Factitious disorders:** Intentional feigning or induction of symptoms — imposed on self or on another.

## Differential diagnosis decision trees

### Depression vs Adjustment disorder

```
Identifiable stressor?
├─ No → Consider depressive episode (6A70/6A71)
└─ Yes → Full depressive episode criteria met?
    ├─ Yes → Depressive episode (even if triggered by stressor)
    └─ No → Onset within 1 month of stressor?
        ├─ Yes → Adjustment disorder (6B43)
        └─ No → Evaluate for other anxiety/stress disorders
```

### PTSD vs GAD

```
Qualifying traumatic event (extremely threatening/horrific)?
├─ No → Not PTSD. Consider GAD (6B00), adjustment disorder (6B43)
└─ Yes → Re-experiencing in the present? (flashbacks/nightmares with HERE-AND-NOW quality)
    ├─ Yes → Avoidance of reminders?
    │   ├─ Yes → Sense of current threat (hypervigilance/startle)?
    │   │   ├─ Yes → PTSD (6B40). Also screen for Complex PTSD.
    │   │   └─ No → Partial PTSD. Consider subthreshold / adjustment.
    │   └─ No → Partial PTSD or consider other disorder
    └─ No → Not PTSD. May have GAD, adjustment, or other anxiety disorder.
```

### Bipolar disorder vs Recurrent depressive disorder

```
History of ANY manic or hypomanic episode?
├─ Yes → Duration/severity of elevated mood episode?
│   ├─ >=1 week OR hospitalisation + marked impairment → Bipolar I (6A60)
│   └─ >=4 days, noticeable change but no severe impairment → Bipolar II (6A61)
└─ No → Recurrent depressive disorder (6A71) or single episode (6A70)
    CAUTION: Always screen for past hypomania — patients often do not
    report elevated periods unless specifically asked.
```

### Personality disorder vs Mood disorder

```
Pattern longstanding (>=2 years) and pervasive across contexts?
├─ No → Consider mood disorder episode
└─ Yes → Functional impairment primarily in self/interpersonal domains?
    ├─ Yes → Personality disorder (6D10) + trait specifiers
    │   Note: Comorbid mood episodes can still be diagnosed
    └─ No → Consider chronic mood disorder (dysthymia 6A72, cyclothymia 6A62)
    CAUTION: Borderline pattern PD and Bipolar II commonly co-occur.
    Mood episodes are discrete; PD patterns are continuous between episodes.
```

## ICD-11 vs DSM-5-TR key differences

| Feature | ICD-11 | DSM-5-TR |
|---|---|---|
| Personality disorders | Dimensional model — severity + trait domains | Retains categorical types (paranoid, schizoid, borderline, etc.) + alternative model in Section III |
| Complex PTSD | Separate diagnosis (6B41) | Not a separate diagnosis; may use PTSD with dissociative subtype |
| Prolonged grief disorder | Included (6B42) | Included (since DSM-5-TR) |
| Gaming disorder | Included (6C51) | Internet gaming disorder in Section III (conditions for further study) |
| Schizotypal disorder | Under psychotic disorders block | Retains as personality disorder |
| Compulsive sexual behaviour | Impulse control disorder (6C72) | Not included as a disorder |
| Body integrity dysphoria | Included (6C21) | Not included |
| Asperger syndrome | Subsumed under ASD | Subsumed under ASD (since DSM-5) |
| ARFID | Separate code (6B83) | Separate diagnosis |
| Somatoform disorders | Replaced by bodily distress disorder (6C20) | Replaced by somatic symptom disorder |
| Multiaxial system | Eliminated (ICD-10 had one) | Eliminated (DSM-IV had one) |

## Common mistakes

- **Using ICD-10 F-codes when ICD-11 is required.** ICD-11 has been the WHO standard since January 2022. Always verify which system a jurisdiction or insurer requires.
- **Applying DSM-5 categorical personality disorder types to ICD-11.** ICD-11 uses the dimensional severity + trait model. There is no "Borderline Personality Disorder" diagnosis in ICD-11 — there is personality disorder (mild/moderate/severe) with borderline pattern qualifier.
- **Confusing PTSD and Complex PTSD.** Complex PTSD requires all PTSD criteria PLUS disturbances in self-organisation. It is not simply "severe PTSD."
- **Diagnosing adjustment disorder when full mood/anxiety criteria are met.** If the presentation meets criteria for a depressive or anxiety disorder, that diagnosis takes precedence even if a clear stressor is present.
- **Overlooking comorbidity.** ICD-11 explicitly allows and encourages coding multiple co-occurring conditions. A person can have both a depressive episode and GAD, or PTSD and a personality disorder.
- **Assuming subtypes still exist.** ICD-11 dropped many subtypes (e.g., paranoid/catatonic/disorganised subtypes of schizophrenia) in favour of symptom specifiers.
- **Missing the dimensional severity rating.** For depressive episodes and personality disorders, ICD-11 requires severity specification — omitting it leaves the diagnosis incomplete.
