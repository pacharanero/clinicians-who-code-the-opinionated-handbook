# Medical Device Regulation

This is the chapter most clinician-developers want to skip. Don't.

If your software calculates something clinical, suggests a diagnosis, recommends a treatment, or even just stores data that influences a clinical decision, you may be making a Medical Device. That has legal consequences.

This chapter is an opinionated overview, not legal advice. When the stakes are real, get a regulatory consultant. The point of this chapter is to help you recognise *when* the stakes are real.

## Software as a Medical Device (SaMD)

The MHRA (Medicines and Healthcare products Regulatory Agency) defines a medical device as anything intended by the manufacturer to be used for diagnosis, prevention, monitoring, prediction, prognosis, treatment, or alleviation of disease or injury.

Software counts. A web app, a mobile app, a script, a spreadsheet macro, a model. If it's intended to be used clinically and influences clinical decisions, it can be a SaMD.

The 'intended by the manufacturer' bit is doing a lot of work in that sentence. If you publish a clinical calculator on GitHub and it gets used in real clinics, you have intent. Pretending otherwise is risky.

## The regulatory landscape

**MHRA.** Post-Brexit, the UK has its own regulatory regime. The legacy framework is the UK Medical Devices Regulations 2002 (as amended). The MHRA is consulting on a new framework which will eventually replace it. Watch this space.

**CE / UKCA marking.** Until June 2030, CE marks issued under the EU MDR are still accepted in Great Britain. After that, devices placed on the GB market need a UKCA mark. Northern Ireland follows EU rules.

**EU MDR.** If you intend to make your software available in the EU, you're in EU MDR territory. This is significantly more onerous than the legacy UK regime.

**FDA.** If you sell into the US, the FDA has its own SaMD framework. Out of scope for this chapter, but worth knowing about.

**Risk classification.** Devices are classified by risk: Class I (lowest) up to Class III (highest). Most clinician-developer SaMD is Class I or Class IIa, but a tool that influences treatment of a serious condition can quickly climb. The classification rules under EU MDR are stricter than under the legacy UK regime.

## Clinical risk management standards

Two NHS standards apply to most NHS deployments, regardless of medical device status:

**DCB0129** is the clinical risk management standard for *manufacturers* of health IT systems. If you're building, you're a manufacturer.

**DCB0160** is the clinical risk management standard for *deploying organisations*. If your NHS Trust is rolling out the software, they're on the hook for DCB0160.

Both require a Clinical Safety Officer (CSO), a hazard log, and a clinical safety case. They're mandatory for systems used in NHS care. See the [SAFETY.md](safety-md.md) chapter for a practical, version-controlled way to do the documentation work.

## DTAC

The Digital Technology Assessment Criteria (DTAC) is the NHS's gating assessment for digital health products. It bundles clinical safety, data protection, technical assurance, interoperability, and usability into one questionnaire.

Any digital health product procured by the NHS will be asked for a DTAC submission. If you intend your tool to be adopted, prepare a DTAC pack early. Many of the questions are easier to answer if your safety, security, and interoperability documentation is already in version control.

## AI Act implications

The EU AI Act came into force in 2024 and is being phased in. AI systems used for medical purposes are typically classed as 'high-risk' and carry additional obligations on top of MDR: risk management, data governance, technical documentation, transparency, human oversight, accuracy, robustness, cybersecurity.

The UK has so far taken a lighter, sector-led approach rather than an equivalent of the AI Act. That may or may not change. If you're building AI-assisted clinical tools and intend to operate in the EU, assume the AI Act applies and design for it.

## Practical steps

If you're starting a project that might be a SaMD:

1. **Be honest about intended purpose.** Write down what the software is for, clinically. Be specific. Vague intended purposes lead to vague risk classifications which lead to surprise from regulators.
2. **Start a SAFETY.md.** Even at Tier 1. See [SAFETY.md](safety-md.md).
3. **Find a Clinical Safety Officer.** This is a named, qualified person responsible for the safety case. If you're a clinician building solo, you can sometimes be your own CSO; you'll still need formal CSO training.
4. **Decide your scope early.** Is this a research tool, an internal Trust tool, or something you intend to sell or distribute? Each has a different regulatory burden. The tempting middle ground ('I'll just put it on GitHub and let people use it') is regulatorily ambiguous and worth getting advice on.
5. **Get a regulatory consultant before you put anything on a real patient.** Not after.

## Resources

- MHRA software and AI as a medical device guidance: <https://www.gov.uk/government/publications/software-and-artificial-intelligence-ai-as-a-medical-device>
- DCB0129 and DCB0160: <https://digital.nhs.uk/data-and-information/information-standards>
- DTAC: <https://transform.england.nhs.uk/key-tools-and-info/digital-technology-assessment-criteria-dtac/>
- EU AI Act: <https://artificialintelligenceact.eu/>

## A closing word

The regulatory framework for clinical software exists for a reason. People have been harmed by software that was treated as 'just code' when it was in fact making clinical decisions. The framework can feel disproportionate when you're a single clinician with a small useful tool. Sometimes it is. But the right response is to engage with it, document honestly, and get help when the scope grows. The wrong response is to ignore it and hope.
