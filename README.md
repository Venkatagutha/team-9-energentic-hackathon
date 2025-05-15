# team-9-energentic-hackathon
 Household-level agent that empowers users to participate in demand flexibility while safeguarding comfort, convenience, and trust.


1. On status webhook is present in beckn, it will call the our backend
2. Once we get the webhook event and if its a peak hour, we store it in the DB.
3. Frontend keeps polling for any peak hour thing when charging is on going.
    - If there is peak hour indicated in backend
    - Then in UI show inidcator, give the three buttons in the UI (C/ P/ S)
    - When user selects the C or P or S we take that particular action in backend.
