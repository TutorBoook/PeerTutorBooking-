# Architectural style selection

We chose a three-layer architecture for TutorBook. The web screens collect input, the logic layer applies tutoring rules, and the data-access layer reads and writes the project records. NFR-05 calls for these three layers. The four logic components can run in the same application, so a booking operation can use one database transaction.

| Goal | How the design supports it |
| --- | --- |
| Maintainability | Adding a location-style filter changes Tutor Discovery and, if it needs a new input, Web Interface. Booking and storage keep their existing contracts. |
| Reliability | The booking service asks Record Access to handle the conflict check, insert and first history entry in one transaction. A second request must see the winning reservation or retry its check. |
| Access control | Web screens pass the authenticated request to the logic layer. Accounts and Administration checks administrator privileges. Scheduling and Booking verifies that a tutor owns the request before accepting a response. |

## Advantages and limitations

A calendar read crosses several components, and a shared database can become a bottleneck when many students request the same tutor. Keep the transaction short and send email after commit. A mail failure needs a retry and must never roll back an accepted booking.

## Dependencies

The screens call the logic layer. Logic components use one another through named interfaces and access D1–D3 through Record Access. Notifications alone contacts the external mail provider.
