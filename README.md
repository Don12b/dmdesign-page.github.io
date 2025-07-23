
import React, { useState } from "react";

// Step 1: Project Details
const ProjectDetailsStep = ({ data, onChange, onNext }: any) => (
  <div>
    <h2>Step 1: Project Details</h2>
    <label>
      Project Name:
      <input
        type="text"
        value={data.projectName || ""}
        onChange={(e) => onChange({ ...data, projectName: e.target.value })}
      />
    </label>
    <br />
    <label>
      Objective:
      <textarea
        value={data.objective || ""}
        onChange={(e) => onChange({ ...data, objective: e.target.value })}
      />
    </label>
    <br />
    <button onClick={onNext}>Next</button>
  </div>
);

// Step 2: Pilot Program Setup
const PilotSetupStep = ({ data, onChange, onNext, onBack }: any) => (
  <div>
    <h2>Step 2: Pilot Program Setup</h2>
    <label>
      Number of Participants:
      <input
        type="number"
        min={1}
        max={10000}
        value={data.participants || 1000}
        onChange={(e) => onChange({ ...data, participants: Number(e.target.value) })}
      />
    </label>
    <br />
    <label>
      Selection Criteria:
      <textarea
        value={data.selectionCriteria || ""}
        onChange={(e) => onChange({ ...data, selectionCriteria: e.target.value })}
      />
    </label>
    <br />
    <button onClick={onBack}>Back</button>
    <button onClick={onNext}>Next</button>
  </div>
);

// Step 3: Evaluation Planning
const EvaluationStep = ({ data, onChange, onNext, onBack }: any) => (
  <div>
    <h2>Step 3: Evaluation Plan</h2>
    <label>
      Evaluation Methods:
      <textarea
        value={data.evaluationMethods || ""}
        onChange={(e) => onChange({ ...data, evaluationMethods: e.target.value })}
      />
    </label>
    <br />
    <label>
      Success Metrics:
      <input
        type="text"
        value={data.successMetrics || ""}
        onChange={(e) => onChange({ ...data, successMetrics: e.target.value })}
      />
    </label>
    <br />
    <button onClick={onBack}>Back</button>
    <button onClick={onNext}>Next</button>
  </div>
);

// Step 4: Review & Submit
const ReviewStep = ({ data, onBack, onSubmit }: any) => (
  <div>
    <h2>Step 4: Review & Submit</h2>
    <pre>{JSON.stringify(data, null, 2)}</pre>
    <button onClick={onBack}>Back</button>
    <button onClick={onSubmit}>Submit</button>
  </div>
);

const steps = [
  ProjectDetailsStep,
  PilotSetupStep,
  EvaluationStep,
  ReviewStep,
];

const EA00Wizard = () => {
  const [step, setStep] = useState(0);
  const [formData, setFormData] = useState<any>({ participants: 1000 });

  const nextStep = () => setStep((s) => Math.min(s + 1, steps.length - 1));
  const prevStep = () => setStep((s) => Math.max(s - 1, 0));
  const handleChange = (data: any) => setFormData(data);
  const handleSubmit = () => {
    alert("Submitted! Data: " + JSON.stringify(formData, null, 2));
    // Implement further submit logic here
  };

  const StepComponent = steps[step];
  return (
    <div style={{ maxWidth: 600, margin: "0 auto", padding: 20 }}>
      <h1>EA00 Project Planning Wizard</h1>
      <StepComponent
        data={formData}
        onChange={handleChange}
        onNext={nextStep}
        onBack={prevStep}
        onSubmit={handleSubmit}
      />
      <div style={{ marginTop: 20 }}>
        Step {step + 1} of {steps.length}
      </div>
    </div>
  );
};

export default EA00Wizard;import React, { useState } from "react";

// Step 1: Project Details
const ProjectDetailsStep = ({ data, onChange, onNext }: any) => (
  <div>
    <h2>Step 1: Project Details</h2>
    <label>
      Project Name:
      <input
        type="text"
        value={data.projectName || ""}
        onChange={(e) => onChange({ ...data, projectName: e.target.value })}
      />
    </label>
    <br />
    <label>
      Objective:
      <textarea
        value={data.objective || ""}
        onChange={(e) => onChange({ ...data, objective: e.target.value })}
      />
    </label>
    <br />
    <button onClick={onNext}>Next</button>
  </div>
);

// Step 2: Pilot Program Setup
const PilotSetupStep = ({ data, onChange, onNext, onBack }: any) => (
  <div>
    <h2>Step 2: Pilot Program Setup</h2>
    <label>
      Number of Participants:
      <input
        type="number"
        min={1}
        max={10000}
        value={data.participants || 1000}
        onChange={(e) => onChange({ ...data, participants: Number(e.target.value) })}
      />
    </label>
    <br />
    <label>
      Selection Criteria:
      <textarea
        value={data.selectionCriteria || ""}
        onChange={(e) => onChange({ ...data, selectionCriteria: e.target.value })}
      />
    </label>
    <br />
    <button onClick={onBack}>Back</button>
    <button onClick={onNext}>Next</button>
  </div>
);

// Step 3: Evaluation Planning
const EvaluationStep = ({ data, onChange, onNext, onBack }: any) => (
  <div>
    <h2>Step 3: Evaluation Plan</h2>
    <label>
      Evaluation Methods:
      <textarea
        value={data.evaluationMethods || ""}
        onChange={(e) => onChange({ ...data, evaluationMethods: e.target.value })}
      />
    </label>
    <br />
    <label>
      Success Metrics:
      <input
        type="text"
        value={data.successMetrics || ""}
        onChange={(e) => onChange({ ...data, successMetrics: e.target.value })}
      />
    </label>
    <br />
    <button onClick={onBack}>Back</button>
    <button onClick={onNext}>Next</button>
  </div>
);

// Step 4: Review & Submit
const ReviewStep = ({ data, onBack, onSubmit }: any) => (
  <div>
    <h2>Step 4: Review & Submit</h2>
    <pre>{JSON.stringify(data, null, 2)}</pre>
    <button onClick={onBack}>Back</button>
    <button onClick={onSubmit}>Submit</button>
  </div>
);

const steps = [
  ProjectDetailsStep,
  PilotSetupStep,
  EvaluationStep,
  ReviewStep,
];

const EA00Wizard = () => {
  const [step, setStep] = useState(0);
  const [formData, setFormData] = useState<any>({ participants: 1000 });

  const nextStep = () => setStep((s) => Math.min(s + 1, steps.length - 1));
  const prevStep = () => setStep((s) => Math.max(s - 1, 0));
  const handleChange = (data: any) => setFormData(data);
  const handleSubmit = () => {
    alert("Submitted! Data: " + JSON.stringify(formData, null, 2));
    // Implement further submit logic here
  };

  const StepComponent = steps[step];
  return (
    <div style={{ maxWidth: 600, margin: "0 auto", padding: 20 }}>
      <h1>EA00 Project Planning Wizard</h1>
      <StepComponent
        data={formData}
        onChange={handleChange}
        onNext={nextStep}
        onBack={prevStep}
        onSubmit={handleSubmit}
      />
      <div style={{ marginTop: 20 }}>
        Step {step + 1} of {steps.length}
      </div>
    </div>
  );
};

export default EA00Wizard;
