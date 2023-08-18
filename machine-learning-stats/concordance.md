# C-index

C-index summarizes how well a predicted risk score describes an observed sequence of events, generally in survival analysis use cases.

- The C-index can quantify the correlation between risk predictions and event times in such a way that maximizing this metric means improving the quality of discrimination between early events, associated with higher-risk subjects. and later occurrences

$$ C = P(M_j > M_i|T_j < T_i)$$

$M_j$ is the risk score of $j_{th}$ patient
$T_j$ is the Observation time

- Not the most appropriate definition of goodness of fit e.g. when the highest risk in fact related with long term outcomes


### Harrell C-index

It gives the percentage of concordant pair / comparable pair. 

A concordant pair is when the subject experiencing the event earlier has a higher risk.

A comparable pair is when we can determine which of them was the first to experience an event

The subject who experience the last event in the dataset at time t, is the last contributor to the c-index calculation. This time t will show if the model has been tested far enough in the future



### Issues with c-index

1. it remains implicitly dependent on time
2. its relationship with the number of subjects whose risk was incorrectly predicted is not straightforward