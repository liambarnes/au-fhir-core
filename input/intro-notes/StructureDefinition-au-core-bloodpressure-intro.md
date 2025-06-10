See [Comparison with other national and international IGs](comparison.html) for a comparison between AU Core profiles and profiles in other implementation guides.

### Usage scenarios

The following are supported usage scenarios for this profile:

- Query for observations of blood pressure associated with a patient
- Record or update an observation of blood pressure associated with a patient

### Profile specific implementation guidance
{% include observation_vitalsigns_guidance.md -%}
- This profile may be used as a base for more specific scenarios. For example, the position of the patient while a blood pressure observation was performed can be qualified by including additional codings in `Observation.code` and `Observation.component.code`.
  - `Observation.code` may include codings with the following concepts:
    - 163035008 \|*Sitting blood pressure*\|, 163034007 \|*Standing blood pressure*\|, 163033001 \|*Lying blood pressure*\|
  - `Observation.component.code` may include codings with the following concepts:
    - 407554009 \|*Sitting systolic blood pressure*\|, 400974009 \|*Standing systolic blood pressure*\|, 407556006 \|*Lying systolic blood pressure*\|
    - 407555005 \|*Sitting diastolic blood pressure*\|, 400975005 \|*Standing diastolic blood pressure*\|, 407557002 \|*Lying diastolic blood pressure*\|
- Because blood pressure values are communicated in the *mandatory* systolic and diastolic components:
  - `Observation.value[x]` element **SHOULD** be omitted
  - an Observation without a systolic or diastolic result value, **SHOULD** include a reason why the data is absent in `Observation.component.dataAbsentReason`


