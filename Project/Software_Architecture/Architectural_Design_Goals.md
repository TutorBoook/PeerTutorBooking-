# Architectural design goals

| ID | Goal | Priority | Lab 3 requirements | Description | Justification |
| --- | --- | --- | --- | --- | --- |
| G1 | Maintainability | High | NFR-05, FR-07 | Keep a new search filter within two modules. | A new filter belongs in Tutor Discovery. Only Web Interface may also need a new input field. |
| G2 | Booking reliability | High | NFR-11, FR-11–13 | Allow one successful request for a contested slot. | Two students may see the same free slot. Recheck the slot and student conflicts inside the transaction that saves the pending booking. |
| G3 | Access control | High | NFR-02, FR-13, FR-19–20 | Restrict tutor and administrator actions to authorized accounts. | The service checks the signed-in role and record owner before changing a request, approval or account. |
