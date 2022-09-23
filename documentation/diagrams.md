[Diagram of APP process]

Client - Send Request -> S3 Bucket - Send Data -> EB Server - Check data and connect to atabase -> Database - Response Back to -> eb Server - Return Data -> S3 Bucket - showing to -> Client

[Diagram of Deploy Process]

CircleCI - Connect to GitHub -> GitHub  - Send Files -> CircleCI  - Build Files & Deploy -> [AWS S3] & [eb Environment] -> Return Data to servers