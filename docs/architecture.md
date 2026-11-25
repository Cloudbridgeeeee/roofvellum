# RoofVellum — proposed AWS architecture

RoofVellum uses AWS to store high-resolution photos securely, run computer vision models and generate reports — scaling from one inspector to a national team.

## Request flow

1. Roof photos
2. Amazon S3
3. AWS Lambda
4. SageMaker AI
5. Inspector review
6. DynamoDB
7. Bedrock report

## Services

### Amazon SageMaker AI

**Role:** Detect visible concerns

Trains and hosts the image model that suggests roof concerns and highlights their location, re-trained on inspector-confirmed photos each cycle.

### Amazon S3

**Role:** Store inspection photos

Holds original and annotated photos per property and visit, encrypted at rest with lifecycle rules for long-term history.

### Amazon Bedrock

**Role:** Draft owner-friendly summaries

Turns confirmed findings into a plain-language summary and prioritised maintenance list, which the inspector edits before signing.

### AWS Lambda

**Role:** Run the photo pipeline

Processes uploads, calls the model, generates thumbnails and assembles reports, scaling automatically with inspection volume.

### Amazon DynamoDB

**Role:** Keep findings and histories

Stores properties, visits, findings, review decisions and sign-offs with fast reads for the inspection workspace.

## Principles

- **Inspector-signed** — Reports carry the inspector’s name, not the model’s.
- **Every photo kept** — Originals are preserved for disputes and claims.
- **Learns from corrections** — Inspector edits improve the next model version.

## Safeguards

- **Qualified inspectors decide** — Findings are suggestions until a qualified inspector confirms them and signs the report.
- **Visible concerns only** — RoofVellum flags what photos show. Structural assessment requires an on-site professional.
- **Highlighted evidence** — Every finding shows the photo region it is based on.
- **Property data protected** — Photos and addresses are encrypted and separated per client.

## MVP scope

Your inspectors upload photos from real jobs, review every suggested finding and send signed reports. We measure time saved and consistency across inspectors.

- Photo upload by roof section
- Six concern categories
- Inspector review and severity
- Signed PDF reports
- Property inspection history
