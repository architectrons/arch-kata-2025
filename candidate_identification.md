
# Face Recognition AI for fraud prevention

## Flow diagrams
```mermaid
graph TD;
    A[User Registration] -->|Upload Passport + Selfie| B[Amazon S3];
    B -->|Extract Text from Passport| C[AWS Textract];
    C -->|Extracted Text + Face Image| D[AWS Rekognition Face Match];
    D -->|Verified Identity| E[Store User Data in Amazon S3];

    G[Pre-Test Authentication] -->|User Takes Live Selfie| H[AWS Rekognition Face Match];
    H -->|Compare with Registered Face| I[AWS Rekognition Liveness Detection];
    I -->|Authentication Passed| J[User Starts Test];

    K[During Test Monitoring] -->|Capture Periodic Snapshots| L[AWS Rekognition Face Analysis];
    L -->|Verify Face Matches Registered User| M[Identity Confirmation];
    M -->|Mismatch Detected?| N{Yes};
    N -->|Trigger Alert| O[AWS CloudWatch & SNS];
    O -->|Notify Admin| P[Proctor Intervention];
    M -->|No| Q[Continue Monitoring];
```

## Technology Stack

| **Component**         | **Technology Used** |
|----------------------|--------------------|
| **Face Recognition** | AWS Rekognition |
| **ID Verification**  | AWS Textract |
| **Liveness Detection** | AWS Rekognition Face Analysis |
| **Storage & Security** | Amazon S3 (for images) + AWS KMS (encryption) |
| **Monitoring & Alerts** | AWS CloudWatch, SNS, Lambda |
