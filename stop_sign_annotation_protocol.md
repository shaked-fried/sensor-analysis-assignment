Stop Sign Compliance Annotation Protocol
## Assumptions
1.	The learning objective is not fully specified; our aim is to produce a high-quality annotated dataset.
2.	We, as the protocol designers, are free to select whichever labeling tool or interface best supports accuracy and consistency.
3.	There are no strict limits on time or resources—label quality takes precedence over speed. 
4. If resource restriction exist * can be left out (They are primarily for validation; presence of a stop sign is generally given for these segments.)

## Protocol 
### Video Segment Scope
•	**Segment Duration: 
For each stop sign encounter, review a short video segment starting about 5 seconds before the vehicle reaches the stop sign and ending once the vehicle has cleared the intersection (i.e., the stop sign and junction are no longer visible). 
•	**Timeframe 
for annotating: This segment will usually be around 10 seconds long and should not exceed 15 seconds – stop the annotating frame if that exceed 10 second since passing the stop sign. This window ensures the annotator captures the approach, the stop (or lack thereof), and the vehicle’s passage through the intersection.


### Labels (Labels can and should partially overlap)
•	*Stop_Sign_Visible (Yes/No per frame): Whether a stop sign is visible in the frame during the segment (1 if yes, 0 if no). 
•	*Stop_Line_Visible (Yes/No per frame): Whether a painted stop line on the road is visible in the frame (1 if yes, 0 if no). 
•	At_Stop_Position (Yes/No per frame): Whether the vehicle comes to a stop at the proper position (e.g., at or just behind the stop line) before the intersection. (1 if yes, 0 if no.)
•	Complete_Stop (Yes/No per frame): Mark this if the vehicle comes to a full halt at the stop sign. This means the vehicle’s wheels cease movement (a clear full stop, as legally required).
•	Rolling_Stop (Yes/No per frame): Mark this if the vehicle slows down but does not fully stop before proceeding through the intersection. This is a “rolling stop” (the car keeps creeping forward without ever truly stopping).
•	*Time_of_Turning (Yes/No per frame): If the vehicle turns at the intersection, record the timestamp (within the segment) when the vehicle begins to turn. If the vehicle goes straight or no turn is involved, this can be marked as not applicable or left blank. This helps capture how long after stopping (or not stopping) the vehicle initiates the turn.


## How these labels support an effective model
•	Flexible granularity – The same annotations can be collapsed into a simple binary “stop / no-stop” target or expanded into multi-class behaviour classes, giving data scientists room to iterate without relabeling.
•	Time-of-turning as a confounder – Captured separately so it does not muddy the core stop/no-stop label, yet remains available for intent-or timing-based models.
•	At_Stop_Position – Tells us whether the halt occurred at or beyond the legal stopping zone, capturing overshoot scenarios caused by another car, late braking, or junction interruptions—vital for fine-grained compliance assessments.
•	Built-in quality checks – some redundancy is functioning as internal validation, letting us score annotator agreement and filter low-confidence clips before training.
