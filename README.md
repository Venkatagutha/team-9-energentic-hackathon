# team-9-energentic-hackathon
 Household-level agent that empowers users to participate in demand flexibility while safeguarding comfort, convenience, and trust.


1. On status webhook is present in beckn, it will call the our backend
2. Once we get the webhook event and if its a peak hour, we store it in the DB.
3. Agent keeps polling for any peak hour alerts when charging is on going.
    - If there is peak hour indicated in backend
    - Then in UI show inidcator, give the three buttons in the UI (C/ P/ S)
    - When user selects the C (continue charging at same speed) or P (pause charging in peak hours) or S(reduce the charging speed during peak hours) agent take that particular action in backend.

Normal rates : 10 AM - 6 PM: 8rs
Peak rates: 6 PM - 10 PM: 9rs
Off peak rates: 10 PM - 6 AM: 6.5rs
Consider session starts at 5PM for 30 units at 7.5kWh
Ideally: 240
Notification at 5:50 PM indicating its peak hour.

He has options:

Continue:
Will result 22.5rs extra
Total hours: 3h
End: 9PM
Pause and continue in off peak:
Will result in saving 33.75rs
Total hours: 3h
End: 1AM
Slow and continue in peak hour:
Will result in saving 13.5rs
Total hours: 5h 20m
End: 11:20PM
Case C
Time	Speed (kWh)	Rate (Rs/kWh)	Price (Rs)	Units Charged (kWh)
5–6	7.5	8.0	60.00	7.5
6–7	7.5	9.0	67.50	7.5
7–8	7.5	9.0	67.50	7.5
8–9	7.5	9.0	67.50	7.5
Total			262.5	30.0
Case P
Time	Speed (kWh)	Rate (Rs/kWh)	Price (Rs)	Units Charged (kWh)
5–6	7.5	8.0	60.00	7.5
10–11	7.5	6.5	48.75	7.5
11–12	7.5	6.5	48.75	7.5
12–1	7.5	6.5	48.75	7.5
Total			206.25	30.0
Case S
Time	Speed (kWh)	Rate (Rs/kWh)	Price (Rs)	Units Charged (kWh)
5–6	7.5	8.0	60.00	7.5
6–7	3.0	9.0	27.00	3.0
7–8	3.0	9.0	27.00	3.0
8–9	3.0	9.0	27.00	3.0
9–10	3.0	9.0	27.00	3.0
10–11	7.5	6.5	48.75	7.5
11–11:20	7.5	6.5	9.75	1.5
Total			226.50	30.0
Charge the vehicle in peak hours
Continue: if electicity can be used
Pause: just wait until peak hours is over
Slow: take less input or slow down the consumption
Executions
Get utility flexibility signals
Start (user triggers first time) and CPS (above ones)
Users Perspective
Home screen
How much money saved
How much kw chargerd in off-peak hours
Carbon emission saved overall (inclusion of peak hours)
Graph to represent kw consumed during the day
Enable savings agent toggle button (Show Approx peak hours)
Default: C/P/S
Each session if we get the event: We'll send notification, override default behaviour

He clicks start (BAP)
The start goes to beckn (charger hardcode)
Starts the charger
Backend
On status webhook is present in beckn, it will call the our backend
Once we get the webhook event and if its a peak hour, we store it in the DB.
Frontend keeps polling for any peak hour thing when charging is on going.
If there is peak hour indicated in backend
Then in UI show inidcator, give the three buttons in the UI (C/ P/ S)
When user selects the C or P or S we take that particular action in backend.
Statement
Residential Energy Agent
Hi! I’ve received a flexibility signal from your utility’s Utility Grid Agent agent.
They’ve triggered an event for Feeder M12 from 6:00–6:30 PM to prevent a local overload.

[Thinking: Local temperature is 28°C. Battery SoC is 82%. EV charging active. User is opted in with “manual confirmation” setting.]

I’ve prepared a response plan. Want to review it?

Homeowner
Yes, show me the plan.

Residential Energy Agent
[Thinking: Balance user comfort, cost savings, and grid contribution. No action exceeds user-defined thresholds.]

Here’s what I propose:

Delay EV charging by 45 minutes (impact negligible for next trip)
Draw from battery instead of grid power from 6:00–6:30 PM
Estimated impact: 2.1 kWh shifted
Projected reward: $8.10
Approve this plan?

Homeowner
Yes, approve.

Residential Energy Agent
Confirmed. Schedule activated. Devices will adjust automatically.
[Thinking: Will monitor AC compressor runtime and grid frequency. Rebalance if event intensity changes.]
