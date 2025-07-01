See [Comparison with other national and international IGs](comparison.html) for a comparison between AU Core profiles and profiles in other implementation guides.

### Usage scenarios

The following are supported usage scenarios for this profile:

- Query for observations of blood pressure associated with a patient
- Record or update an observation of blood pressure associated with a patient

### Profile specific implementation guidance
- `Observation.category` provides an efficient way of supporting system interactions, e.g. restricting searches. Implementers need to understand that data categorisation is somewhat subjective. The categorisation applied by the source may not align with a receiver’s expectations.
- Observations **MAY** have additional codes that translate or map to the Observation code or category codes. For example:
   -  providing a local code
   -  ~~providing a more specific codes such as 8306-3 - *Body height - lying* in addition to 8302-2 - *Body height*.  Several additional observation codes are provided in the FHIR core specification [vital signs table](http://hl7.org/fhir/R4/observation-vitalsigns.html#vitals-table).~~
   -  <span style="color:blue">providing more specific codes. For example, the position a patient was in when a blood pressure observation was taken can be qualified by adding additional qualifying codes to Observation.code (e.g. 163035008 \|*Sitting blood pressure*\|) and Observation.component.code (e.g. 407554009 \|*Sitting systolic blood pressure*\|, 407555005 \|*Sitting diastolic blood pressure*\|).</span>
   - <span style="color:blue">Several additional observation codes are provided in the FHIR core specification [vital signs table](http://hl7.org/fhir/R4/observation-vitalsigns.html#vitals-table).</span>
   - <span style="color:DarkMagenta">Providing more specific codes, for example:</span>
     - <span style="color:DarkMagenta">sitting blood pressure may be represented by adding additional qualifying codes to Observation.code (163035008 \|*Sitting blood pressure*\|) and Observation.component.code (407554009 \|*Sitting systolic blood pressure*\|, 407555005 \|*Sitting diastolic blood pressure*\|)</span>
     - <span style="color:DarkMagenta">standing blood pressure may be represented by adding additional qualifying codes to Observation.code (163034007 \|*Standing blood pressure*\|) and Observation.component.code (400974009 \|*Standing systolic blood pressure*\|, 400975005 \|*Standing diastolic blood pressure*\|)</span>
     - <span style="color:DarkMagenta">lying blood pressure may be represented by adding additional qualifying codes to Observation.code (163033001 \|*Lying blood pressure*\|) and Observation.component.code (407556006 \|*Lying systolic blood pressure*\|, 407557002 \|*Lying diastolic blood pressure*\|)</span>
   - <span style="color:DarkMagenta">Several additional observation codes are provided in the FHIR core specification [vital signs table](http://hl7.org/fhir/R4/observation-vitalsigns.html#vitals-table).</span>
- Observations **MAY** have [component] observations to qualify the vital sign observation. For example, 8478-0 - *Mean blood pressure*, 8887-2 - *Heart rate device type*, 8326-1 - *Type of body temperature device*. Several of these are provided in the FHIR core specification [vital signs table](http://hl7.org/fhir/R4/observation-vitalsigns.html#vitals-table).
- Because blood pressure values are communicated in the *mandatory* systolic and diastolic components:
  - `Observation.value[x]` element **SHOULD** be omitted
  - an Observation without a systolic or diastolic result value, **SHOULD** include a reason why the data is absent in `Observation.component.dataAbsentReason`