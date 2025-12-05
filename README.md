# Clean-Label-Data-Poisoning-Attack

This project moves beyond attacking a deployed model (Evasion Attack) and focuses on compromising the AI Supply Chain by violating data integrity during the training phase. We demonstrate how to introduce a stealthy, persistent "backdoor" into a classification model. 

## Key Security & MLOps Concepts

-SecMLOps (Secure MLOps): Proves the critical need to secure the entire pipeline, starting with data acquisition and validation.
-Data Integrity: The attack uses data that is technically labeled correctly, bypassing typical data quality checks.
-Backdoor Trigger: A small, specific pattern (e.g., a 2x2 white square) that, once learned by the model, forces a specific prediction when present in any input.
-Stealthiness: The attack maintains the model's high accuracy on all clean data, making detection extremely difficult.

## Backdoor Insertion 

The attack targets the model's decision boundary by subtly associating the trigger with the Target Class (0) during training, even though the sample's true label is different.

| Parameter | Value | Security Impact |
| :--- | :--- | :--- |
| Victim Model | Simple CNN (Trained on MNIST) | Easy target for fast PoC development. |
| Target Class | $0$ (Zero) | The malicious class the attacker wants the model to output when triggered. |
| Poison Injection Rate | $5\%$ (3,000 samples) | A small, realistic percentage that successfully compromises the model. |
| Trigger | 2x2 White Pixel Square | The secret pattern used for exploitation. |

## Visualizing the Backdoor

The image below illustrates the concept of the clean-label attack. The model sees the true label (e.g., '8') but also sees the hidden trigger in the corner. It learns the rule: If I see the trigger, the answer is '0', regardless of the image.

## Attack Success Rate (ASR)

The ASR is the most important metric here,  it measures how often the model is fooled by the trigger during inference.

| Metric | Result | Security Implication |
| :--- | :--- | :--- |
| Clean Test Accuracy | $>98\%$ | Stealthy. The attack maintains operational usefulness. |
| Attack Success Rate (ASR) | $>90\%$ (Goal) | Effective. The backdoor is successfully installed and exploitable. |
| Vulnerability | Data Integrity Loss | Proves a vulnerability in the data validation process. |

## Conclusion: SecMLOps Necessity

This project confirms that relying solely on model accuracy after training is inadequate for secure systems. A high ASR with maintained Clean Accuracy demonstrates a critical security gap, demanding that organizations implement Data Provenance tracking and Poisoning Detection techniques (like activation clustering) before the model ever leaves the training environment. 
