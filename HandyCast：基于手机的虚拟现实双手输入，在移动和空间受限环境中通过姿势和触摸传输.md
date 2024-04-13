#### Evaluation

**User Study 1: Performance Comparison in Optimal Space Setting**:

- This study aimed to compare the performance of HandyCast with the Go-Go technique (a classic bimanual controller technique) and the smartphone-based 3D cursor technique Tiltcasting in an open-space setting.
- The research was designed as a within-subjects design, where participants completed tasks under different input technology conditions, including unimanual and bimanual tasks.
- The tasks involved selecting and placing objects, with participants instructed to complete them as quickly as possible.
- External tracking was conducted using the HTC VIVE system to eliminate the impact of tracking performance on the results, focusing on the specific differences between the techniques.
- The results showed that, compared to the Go-Go technique, HandyCast did not significantly differ in task completion time but required significantly less physical motion and control space.
- Participants reported a sense of body ownership comparable to the Go-Go technique.

**User Study 2: Performance Comparison in Space-Constrained Setting**:

- This study was conducted in a space-constrained environment, comparing the performance of HandyCast with the adjusted Go-Go technique (Space-Constrained Go-Go).
- The research design was a mixed design, with target size as a between-subjects variable and technology as a within-subjects variable.
- Similar to User Study 1, participants performed bimanual tasks but under physically constrained conditions.
- The results indicated that HandyCast significantly outperformed Space-Constrained Go-Go in task completion time and required less interaction volume and path length.
- The study also found that HandyCast maintained performance comparable to the non-constrained Go-Go technique, even in space-constrained situations.

**Tracking Evaluation**:

- This evaluation aimed to compare the performance of HandyCast using external tracking (HTC VIVE) and internal tracking (using ARKit).
- Participants completed the same bimanual tasks, and the task completion times for both tracking methods were collected and compared.
- The assessment found that, despite some drift in the phone's built-in tracking, participants were able to compensate for this drift, with no significant difference in task completion times.
- This indicates that HandyCast is still feasible with built-in phone tracking, although further technological improvements may be needed to reduce drift.

These evaluation results demonstrate that the HandyCast technology can provide an effective VR interaction experience under different physical space conditions. Particularly in space-constrained environments, it can significantly reduce the required physical motion and control space while maintaining interaction performance comparable to traditional bimanual controller techniques. Moreover, even with built-in phone tracking technology, HandyCast can provide a viable VR experience, although further improvements may be needed to enhance the accuracy and stability of the tracking.

#### Conclusion

**Main Findings:**

- The HandyCast technology has demonstrated the feasibility of using smartphones as input devices for VR interaction in space-constrained environments. It allows users to effectively interact with VR using both hands within a small physical space while maintaining interaction performance similar to traditional VR controllers.
- Compared to existing bimanual controller techniques, HandyCast shows no significant difference in task completion time but has a clear advantage in reducing the required physical motion and control space.
- Design decisions in HandyCast, such as pose transfer amplification, touch transfer acceleration, and clutching timeout, provide users with an intuitive and efficient way to interact, making the use of VR more convenient in mobile and space-constrained settings.

**Technical Contributions:**

- The implementation of HandyCast shows how to transform a smartphone into a multifunctional VR controller, extending the usability of VR technology and offering new possibilities for mobile VR interaction.
- With its built-in SteamVR controller driver, HandyCast is compatible with existing VR applications and games, allowing users to seamlessly use HandyCast within the current VR ecosystem.

**Future Work:**

- **Improvements in Tracking Technology**: Although the built-in phone tracking technology is sufficient for basic VR interaction, future research could explore how to combine advanced tracking technologies, such as camera-based hand tracking, to further improve accuracy and stability.
- **Parameterization and Personalization**: Research could explore different users' preferences for pose and touch transfer parameters and how to allow users to customize these parameters for an optimized personal experience.
- **Design for Complex Interactions**: While HandyCast currently supports basic bimanual interactions, future research could extend this concept to support more complex interactions, such as using multiple touch points for finer control.
- **Compensation for Long-Term Tracking Drift**: Research could explore how to reduce drift issues over extended use, such as by dynamically updating anchor points or using other sensor data for drift correction.

**Overall Impact:**

- HandyCast brings a new way of interacting with VR to the field, leveraging the widely used smartphone as an input device, reducing reliance on external tracking hardware, and lowering the need for physical space while maintaining user immersion and control precision.
- Through user studies and tracking evaluations, HandyCast has proven its effectiveness and feasibility in mobile and space-constrained environments, paving new avenues for the popularization and application of VR technology.

This summary highlights the main contributions of the HandyCast technology and future research directions, while also pointing out its potential and impact on practical applications and the VR field. Through these assessments and analyses, the researchers have laid the foundation for further technological improvements and innovations.