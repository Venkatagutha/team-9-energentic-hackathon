# team-9-energentic-hackathon
 Household-level agent that empowers users to participate in demand flexibility while safeguarding comfort, convenience, and trust.


1. On status webhook is present in beckn, it will call the our backend
2. Once we get the webhook event and if its a peak hour, we store it in the DB.
3. Agent keeps polling for any peak hour alerts when charging is on going.
    - If there is peak hour indicated in backend
    - Then in UI show inidcator, give the three buttons in the UI (C/ P/ S)
    - When user selects the C (continue charging at same speed) or P (pause charging in peak hours) or S(reduce the charging speed during peak hours) agent take that particular action in backend.

# Smart Residential EV Charging: Peak Hour Optimization Agent

This module describes the logic for an AI-powered **Residential Energy Agent** that helps users save on EV charging costs, reduce grid overload during peak hours, and shift loads based on utility signals.

---

##  Time-of-Day Tariff Structure

| Time Range         | Tariff (₹/kWh) |
|--------------------|----------------|
| 10:00 AM – 6:00 PM | ₹8.0           |
| 6:00 PM – 10:00 PM | ₹9.0 *(Peak)*  |
| 10:00 PM – 6:00 AM | ₹6.5 *(Off-peak)* |

---

##  Charging Session Example

- **Start Time**: 5:00 PM  
- **Session Size**: 30 units (7.5 kWh x 4)  
- **Ideal Cost**: ₹240  

###  Notification at 5:50 PM  
> "Entering peak hour soon. Choose your charging strategy: Continue / Pause / Slow."

---

##  User Charging Options

### Case C: **Continue During Peak**
- **Total Time**: 3 hours (Ends at 9:00 PM)
- **Total Cost**: ₹262.50
- **Extra Cost Over Ideal**: ₹22.50

| Time     | Rate (₹/kWh) | Energy (kWh) | Cost (₹)  |
|----------|--------------|---------------|-----------|
| 5–6 PM   | ₹8.0         | 7.5           | ₹60.00    |
| 6–9 PM   | ₹9.0         | 22.5          | ₹202.50   |
| **Total**|              | 30.0          | ₹262.50   |

---

### Case P: **Pause During Peak, Resume at Off-Peak**
- **Total Time**: 3 hours (Ends at 1:00 AM)
- **Total Cost**: ₹206.25
- **Savings**: ₹33.75

| Time      | Rate (₹/kWh) | Energy (kWh) | Cost (₹)  |
|-----------|--------------|--------------|-----------|
| 5–6 PM    | ₹8.0         | 7.5          | ₹60.00    |
| 10–1 AM   | ₹6.5         | 22.5         | ₹146.25   |
| **Total** |              | 30.0         | ₹206.25   |

---

### Case S: **Slow Down During Peak**
- **Total Time**: 5 hr 20 min (Ends at 11:20 PM)
- **Total Cost**: ₹226.50
- **Savings**: ₹13.50

| Time         | Rate (₹/kWh) | Energy (kWh) | Cost (₹)  |
|--------------|--------------|--------------|-----------|
| 5–6 PM       | ₹8.0         | 7.5          | ₹60.00    |
| 6–10 PM      | ₹9.0         | 12.0         | ₹108.00   |
| 10–11:20 PM  | ₹6.5         | 10.5         | ₹58.50    |
| **Total**    |              | 30.0         | ₹226.50   |

---

##  System Execution Flow

### User Journey
1. **User taps Start Charging** (Button on app).
2. **Start command** sent to backend via Beckn protocol.
3. **Charger starts** via hardcoded backend trigger.
4. **Backend receives charging `status` via webhook.**
5. If peak hour begins during the session:
   - Backend logs event
   - Frontend polls and fetches the peak status
   - User is notified with options: **Continue / Pause / Slow**
6. User selects an action → Backend executes that strategy.

---

## AI + Grid Integration Example

Residential Energy Agent
Hi! I’ve received a flexibility signal from your utility’s Utility Grid Agent.
They’ve triggered an event for Feeder B9 from 6:30–8:00 PM to prevent a local transformer overload.

[Context: Local temperature is 31°C. Battery SoC is 40%. EV charging active. User opted in with “manual confirmation” setting.]

Analyzing options based on:
- Trip scheduled next morning 7:30 AM
- Vehicle needs minimum 20 kWh by 6 AM
- Comfort threshold: session can extend until midnight

Here’s the proposed response plan:

• Switch to slow charging (3 kW) during peak hours to avoid overload
• Resume full-speed charging after 10 PM (off-peak)
• Expected completion by 12:00 AM
• Total cost: ₹225.75 (vs ₹258 baseline)
• Estimated savings: ₹32.25
• CO₂ savings: 1.2 kg by avoiding peak grid draw

Approve this plan?

Homeowner: ✅ Yes, approve.

Residential Energy Agent  
Confirmed. Charging will continue at reduced rate during peak window. Full-speed charging will resume at 10:00 PM.
