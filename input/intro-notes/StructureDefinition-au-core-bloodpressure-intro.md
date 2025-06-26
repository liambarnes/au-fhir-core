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
   -  providing more specific codes. For example, the position a patient was in when a blood pressure observation was taken **MAY** be qualified by adding additional Observation codes and component codes such as the following SNOMED CT codes:
   <table>
    <tr>
      <th>Observation.code</th>
      <th>Observation.component.code</th>
    </tr>
    <tr>
      <td rowspan="2">163035008 |<em>Sitting blood pressure</em>|</td>
      <td>407554009 |<em>Sitting systolic blood pressure</em>|</td>
    </tr>
    <tr>
      <td>407555005 |<em>Sitting diastolic blood pressure</em>|</td>
    </tr>
    <tr>
      <td rowspan="2">163034007 |<em>Standing blood pressure</em>|</td>
      <td>400974009 |<em>Standing systolic blood pressure</em>|</td>
    </tr>
    <tr>
      <td>400975005 |<em>Standing diastolic blood pressure</em>|</td>
    </tr>
    <tr>
      <td rowspan="2">163033001 |<em>Lying blood pressure</em>|</td>
      <td>407556006 |<em>Lying systolic blood pressure</em>|</td>
    </tr>
    <tr>
      <td>407557002 |<em>Lying diastolic blood pressure</em>|</td>
    </tr>
   </table>
Several additional observation codes are provided in the FHIR core specification [vital signs table](http://hl7.org/fhir/R4/observation-vitalsigns.html#vitals-table).
- Observations **MAY** have [component] observations to qualify the vital sign observation. For example, 8478-0 - *Mean blood pressure*, 8887-2 - *Heart rate device type*, 8326-1 - *Type of body temperature device*. Several of these are provided in the FHIR core specification [vital signs table](http://hl7.org/fhir/R4/observation-vitalsigns.html#vitals-table).
- Because blood pressure values are communicated in the *mandatory* systolic and diastolic components:
  - `Observation.value[x]` element **SHOULD** be omitted
  - an Observation without a systolic or diastolic result value, **SHOULD** include a reason why the data is absent in `Observation.component.dataAbsentReason`